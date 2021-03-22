---
layout: post
title:      "CLI Gem Project w/ GraphQL"
date:       2021-03-22 04:17:46 +0000
permalink:  cli_gem_project_w_graphql
---


This was certainly an adventure. I will preface this with saying that I was very nervous going into this project. It was obviously the first one in the course. It's not like I have no experience with coding projects either but I really wanted to challenge myself and make something that I could actually use in my day-to-day. When I am not at my day job or grinding out these labs, I run fighting game tournaments. Yes, like Street Fighter or Smash. I actually organize and produce all of the TSB events here in NYC for games like Guilty Gear and Blazblue. So right off the bat I wanted to build something that I could mix into this. A lot of players, commentators etc wanted a way to review the set history between players. With how often some of the top players play each other, it's always good to see "Hey, this person has won the last 4 times they played against this other person!". That's where the idea for this app came. 

### Challenges
Right off the bat, I thought I was being overly ambitious. I tend to do this a lot but even before I started I was hit with a few big walls that I was not sure how to overcome:
* How do I even start?
* What on earth is GraphQL? How do I work with this ALPHA api?
* Once I manage to get the data, how far should I go with it?


If I'm honest, I had a few back-up plans in case this was too difficult and I had to give it up. Starting was a challenge. Before this, we never really started a project from scratch so I was not sure where to go. Luckily, the course directed me to the Eden Project which starts off answering the question "Where do I start?". It was a good reminder for me to actually read all of the instructions and watch all of the videos before bashing my head against the wall for a few hours. 

The site that hosts most of the tournaments is called Smash.gg. The API itself uses something called GraphQL. The actual definition is: "GraphQL is an open-source data query and manipulation language for APIs, and a runtime for fulfilling queries with existing data". Forgive me if I am years behind on this but I had never heard of this. I've worked with REST-API at my full time job briefly. At the very least I understand the gist of it. This GraphQL was supposed to be kind of similar I guess. It was actually very cool. Once I got in the groove of how it worked, I spent a lot of time in the API explorer for smash.gg just pulling all kinds of data and trying to find the limits of what I could do with my project. I quickly ran into a few issues that were a result of the API being in an alpha state. One example was when you have the PLAYER object and you tried to find their SETS, if you try to display more sets than they have, it will display nothing. This was a huge problem because players can have...5 sets to 100+ (especially for the older games). I felt like a genius finding the work around. Rather than getting the sets via the PLAYER object, I found a player's EVENTS and pulled the sets from there but filtered to just the player. For some reason, this worked with the API and it did not bomb out when the number of sets to display was higher than the number of sets had. 

Now I have all this data. What do I do? I already had a clue of what I wanted. I just was not sure how much of it I can resonably do for a project. I decided to keep it simple and just get the sets the player participated in. I used everything we learned so far with Ruby to create the necessary objects to represent Player, Sets, Tournament and CLIManager. Then I ran into another issue I should have seen coming. How do I take my GraphQL query and use it in Ruby? This was difficult. There is a Ruby gem for GraphQL so I thought I would just gem install then call a method named #GraphQL::Query and call it a day. Unfortunately, it was not that easy. I could not find anything that would help me with this until I looked at some sample code on the Smash.gg site in python and thought to myself "This *kind of* looks like a RESTAPI call. I looked into HTTParty (awesome name by the way) and found a blog post from 4 years ago showing how to make a GraphQL call with HTTParty. Shoutouts to that guy. For anyone in the future trying to find how to do this, I hope this helps:

```
@url = 'https://api.smash.gg/gql/alpha'
@token = 'wae3qe3124323raesr324ad'

query = %{
query Users($slug: String) {
 user(slug: $slug) {
  genderPronoun
  location {
   state
   country
  }
  authorizations(types: [TWITCH, TWITTER, DISCORD]) {url}

  player {
   id
   gamerTag
   sets(perPage: 1, page: 1) {
    nodes {
     displayScore
     fullRoundText
     event {videogame {displayName}
      tournament {name}
     }
    }
   }
  }
 }
}}

variables = {
    slug: "356d0e24"
  }


result = HTTParty.post(
  @url,
  headers: { 
    'Content-Type'  => 'application/json', 
    'Authorization' => "Bearer #{@token}" 
  },
  body: { 
    query: query, 
    variables: variables 
  }.to_json
)

puts "#{result}"
```

### Final Thoughts
There are some things I wish I did better. I think my code is honestly a bit complicated. I am not sure how to simplify it though. The nature of the project itself is pretty complex because it is scraping data from somewhere that is constantly changing or is incomplete depending on where you pull it from. So there are a lot of conditionals to make sure, for example, that a user actually has a social media link in their profile. This is to prevent the code from bombing out when it tries to access a variable that is nil. I think I could have handled errors better rather than doing things like 
```
 unless set_exists?(id)
   # Do a lot of things
end
```

I am not sure what best practice is regarding that. It's just what I am most used to at my current job (we code very loosly there). I tried my best to allow for modifications in the future incase I want to add more functionality or even add other bracket-running APIs like Challonge.com or the new Fb.gg. I ran into a lot of small bugs but I felt that all of the lessons before hand, prepared me for a lot of these. My personal goal for taking this course is to become more confident in my ability to code. I won't give my entire auto-biography but I will say with this project, I challenged myself and succeeded and feel pretty damn good about it. Excited to see what's next!
