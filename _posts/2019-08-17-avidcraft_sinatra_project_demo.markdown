---
layout: post
title:      "AVIDcraft | Sinatra Project Demo"
date:       2019-08-17 19:03:20 +0000
permalink:  avidcraft_sinatra_project_demo
---

For my second project at [Flatiron](https://flatironschool.com/), I worked with Sinatra, ActiveRecord, and SQL to build a web application with database capabilities that utilizes encryption and sessions.  This project went much smoother than my experience with the first project!  I had a better understanding of what was expected and also a better grasp on the content we had learned.  I know I will encounter many learning edges and uncomfortablility when when I get to the presentation aspect of this project, but I at least feel more comfortable with the expectations and can better prepare.  All normal things that are apart of this process of learning something new!

The inspiration for this project comes from life experience.  As long as I can remember, I have worked as a craftsperson in one realm or another.  Whether it be general making, craft business ownership, management, retail sales, or overseeing techincal setup at my local art gallery-- I have always had hands-on involvement in some type of craft capacity.  As a youngster, I was always making something-- whether it be paper to draw on, or friendship bracelets and squishy stress balls to sell to my peers (the stress balls were made with flour and balloons and some of them might have exploded on people, but hey, failure is a part of the process!).  Taking my experience into consideration, I was inspired to create an application that allows people to create an account and list the handmade items they've created.

I kicked off this project, by making a bunch of lists.  I've learned over time that I process, remember, and work best when I can write down what needs to be done.  Where speaking and presenting can easily send my mind into chaos, writing down the information and tasks helps me to slow down and sort out my thoughts, and from that space I can better focus on the muscle memory needed to more fluidly talk about a subject.  So, I hit the pad and pencil and jotted down all the project requirements as well as the initial file structure and starter methods I would need to make this app function.  I took these initial thoughts and typed them up in a Google Doc where I could easily organize and manipulate the items into a more ordered list.  Then what did I do?  I re-handwrote the list. (:  From that list I wrote out a few post-it notes that ordered the inital milestones I wanted to hit within development.  This project mapping of sorts helped me put all the pieces together and from there, I felt ready to begin the actual coding process.

Here's the list I used to start my project:
1. Set up git.
2. Set up project file structure.
3. Set up Gemfile, bundle install.
4. Set up environment.rb and config.ru files.
5. Go ahead and setup my Rakefile and License file.
6. Setup ApplicationController and run a Shotgun test.
7. Setup my other controllers: UsersController, ItemsController
8. Model setup: User, Item.
9. Initial HTML setup for layout and index pages, and get route to make sure navigation is funtioning properly, run another Shotgun test.
10. Database setup and migrations; run a pry test.

After completing these 10 tasks I was able to more or less work through setting up the rest of my application in auto-pilot mode by utilizing previous code templates I'd saved, notes from my notebook (I write down all the lessons in my own shorthand), and Google.  Utilizing Rake and pry I set up a user in my database and from there was able to use that test object to setup the initial login and logout routes and the coordinating pages within my application.  Testing out my methods via shotgun, I moved on to add functionality for creating a user.  From there it was on to the items: creating a new item, then editing, viewing, and deleting. Password and sessions is a project requirement for our users, therefore I had to make sure that a user could only edit an item they created.  I also had to make sure my application properly communicates to the user any errors, whether that be at account creation, login, or item creation and edit.  I finished up by working on the asthetic of the app-- layout, fonts, colors!  Logo design!  I had a fun time working out those last bits.  

Up until I was ready to submit (even while filming the demo of my project!) I kept finding little things that I could refactor or edit or tinker with, which seems like a common problem in creating an application.  And of course there are a few things I didn't get to, which would have made my application better or more secure, simply because I knew I would need a lot of time to focus and prepare for the presentation aspect of this project, which was a really important goal for me this time around!  Overall, I am very pleased with the application I have created and look forward to learning more.  

For your viewing pleasure, below is the video walk through of my application, and the repo can be found [here](https://github.com/reneenordholm/avidcraft).  Cheers!

<iframe width="560" height="315" src="https://www.youtube.com/embed/JLzPDccj2g8" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>


 






