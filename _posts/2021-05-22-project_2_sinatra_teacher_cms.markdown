---
layout: post
title:      "Project 2: Sinatra + Teacher CMS"
date:       2021-05-22 21:28:57 +0000
permalink:  project_2_sinatra_teacher_cms
---


## Deciding what on earth to do
This project was definitely an interesting one. While it felt like we had the same amount of freedom with deciding what to do, I felt like if I got TOO ambitious, it would quickly escalate into a mess of a project. So first step was choosing the domain. I went through my head like "What do I know about?". I know about video game tournaments. It is basically a second job for me. I wanted to expand beyond that though since my first project was video game related. What else is there? My full-time job has me working with schools very often. I am very familiar with the dynamic of teachers and students even though I do not work directly with them. I settled on the educational domain with my models being Teachers, Students, and Courses. I figured I could create like a mini Google Classrooms. 

## Challenges
The challenge here was deciding how much the user (teachers) could do. I tried to keep it realistic. Usually a teacher does not onboard themselves but for the sake of this project I decided they can sign-up for an account. Now, were they going to manage the courses or the students? I tried to approach this as if it were a real life scenario. Typically, students are brought in from an external system like eSchool or Powerschool. Again for the purpose of this project I had the option of creating a student (one at a time) and seeding the majority of them. The only reason I had the option of letting teachers create students was because I always thought that would be convinient. No other reason (lol). The teachers should not have the ability to delete students though. That is left to administrators in most cases. Moving along to courses, for the purpose of this project, this is what we will be CRUD-ing (is that a term? I'm sorry if not). A teacher should have access to managing their course. Creating a new one and choosing students from a list to add them to sounds like a real scenario. Most likely, again, this is probably managed by administrators. In my case here, I wanted teachers to be in control of their courses, without being able to modify anyone elses courses. 

Another issue I ran into was actually with Sinatra itself. I ran into a bug that I could not solve for the life of me. All I wanted to do was create a nav bar (a lazy one but still functional). I got an error that was something like "errno:eio input/output error". Everything I looked up mentioned something about making sure the paths to the view are all correct in the controllers. I checked and checked and it still did not work. Eventually I cam across a post that mentioned that it is a linux error. "In linux EIO means, that there was made an attempt to read/write to stream which is currently unavailable. This could happen because of physical error or when orphaned process (whose parent has died) attempts to get stdio from parent process, or when stream is closed."

Once I switched the port I was running shotgun on it worked. Hurray! EXCEPT I SPENT HOURS ON THIS. I was ready to lose my mind. But alas, that is programming in a nutshell. 


## Final Thoughts
I think in my code is very easy to understand, ActiveRecord is something I am very new to and I am honestly just amazed at how powerful it is. So many times throught this course I because doing things "the long way" only to find out ActiveRecord already handled that. An example was getting Courses from Students. Initially, I would have done something like:

Get Student.id
Pull every course
Map to an array courses every course that had the student_id in it. 

So much work! ActiveRecord lets me just do student.courses. It's magic to me. Very cool and excited to learn about other powerful frameworks!
