---
layout: post
title:      "CLI - Project (First Big Project) Day 1-2"
date:       2021-03-15 17:53:01 +0000
permalink:  cli_-_project_first_big_project_day_1-2
---


I'll preface this by saying that I am not a writer whatsoever. I did my best to skip every writing class in school and college as I could. I am only doing this because I think it is a requirement for the CLI Project. Honestly though, it might do me some good to write down my thoughts as I progress on this. I'm sorry ahead of time for all the typos and errors I will make (If anyone ever reads this)

I've given the project some thought before-hand but these past two days were when I finally hunkered down to plan everything out. To preface, I thought about what I could make that would be useful to me. I organize and produce video game tournaments (fighting games in particular). I figured it would be helpful for the commentary team to have information before a match like:

Player 1 vs Player 2 
Player 1: 6 Wins
Player 2: 2 Wins

Something like that to show who's won previous encounters. To make it fit he scope of the project I'll also allow for the user to get additional information. 

HERE IS WHERE IT GETS TRICKY. 

The api we are using is for Smash.gg, the tournament running site. It's not bad. You query for the user and are able to bring back a lot of information. The issue lies with the rate-limit of the API. I may be able to request a higher rate limit. It will be worth a shot. 

I'm sure I will run into many issues along the way. First step is to set up my environment correctly. I would like to be able to use rspec with this project for testing but I am not sure if it is needed. For now, I'll take it slow and go bit by bit.
