---
layout: post
title:      "Horoscope Reader -- Ruby CLI Project"
date:       2019-06-17 00:59:20 +0000
permalink:  horoscope_reader_--_ruby_cli_project
---


For my first Ruby project, built as part of the [Flatiron](https://flatironschool.com) part-time online-based curriculum, I chose to build a horoscope reader that would use data from the [Horoscope.com](https://www.horoscope.com) website.  The program first scrapes data from the website to give the user 12 astrological signs to choose from and then asks the user to select the number associated with the sign in which they would like to read the horoscope.  

Upon selecting the sign, the program then scrapes a second level of data from the website, which outputs the day's horoscope for the chosen sign.  After displaying the horoscope it asks the user whether or not they woud like to view another sign's horoscope.

By answering Y, the programe will return to the main menu and display the 12 astrological signs, again asking the user which sign they would like to see.

By answering N, the program tells the user 'Goodbye' and exits.

![](https://raw.githubusercontent.com/reneenordholm/horoscope_reader/master/Blog/cli_screenshot.png)

What is happening behind the scenes to make this happen? Let's take a step-by-step  walk through the backend of this CLI program to get a better understanding of how everything comes together.  It all starts with the foundation of the program, which is located in the bin, short for binary, folder.  From here the files in this folder extend to other files, giving them direction on how to proceed. 

![](https://raw.githubusercontent.com/reneenordholm/horoscope_reader/master/Blog/ruby_cli_image_1.png)

Using Bundler to do the initial setup of our gem handily creates these basic files and folders, but we still must customize them to coordinate with our gem's specs.  The *setup* file tells the operating system it will need to install our bundle of files and folders before proceeding.  The *console* file tells the operating system it will need to setup the files using Bundler and also that it will need the our program's main folder, 'horoscope_reader,' and it's contents.  It all comes together in the *run* file, which brings together the knowledge of the *setup* and *console* files to instantiate a new instance of the program and in order to do that it will need to checkout the *environment.rb* file and the CLI class within the *cli.rb* file, which are both located in the lib, short for library, folder.

Before we proceed to the lib folder, let's touch base on a few key terms:
* The difference between `require` and `require_relative`: Our program is merely a web of connected files and folders contained within a master folder.  In order to ensure the listed method operates, these connected files and folders need instruction to know where the other files and folders they should call on to access information are located. If the file to be called is located within the same folder as the file currently being operated on, these files can be called on by including the `require` command and designating the file within quotes.  If the file is located within a separate folder, we will need to use the `require_relative` command to let the system know to exit out of the folder it is currently in and look in a different folder.
* No we are not writing lyrics for a Ricky Martin song!  A *shebang* is the code heading all the files in our bin folder, `#!/usr/bin/env ruby`, it lets the operating system know it should use Ruby in order to read any of the information located within our program's files and folder.
* We can have all this fancy code but none of it will work if we don't birth a new version of it.  Hence `.new`.  By calling `.new` on a class it creates a new object, or version of the program, for us and from there moves us on to the next step!  

![](https://raw.githubusercontent.com/reneenordholm/horoscope_reader/master/Blog/ruby_cli_image_2.png)

Our lib folder has the fun task of holding all our actionable files.  This is where our code lives that when the `.new` object is instantiated, runs over to, to see what the next step is.

![](https://raw.githubusercontent.com/reneenordholm/horoscope_reader/master/Blog/ruby_cli_image_3.png)

First we'll stop at the *environment.rb* file where we'll get an initial overview of the files, folders, and gems needed in order for our program to function.  Notice our `require` and `require_relative` commands that direct us on where to look next.

Curious about `pry`, `open-uri`, and `nokogiri`?  We'll learn about those later when we explore our *gemfile*. For now, let's move on to our *cli.rb* file so we can start digging deeper on how this program really works!

![](https://raw.githubusercontent.com/reneenordholm/horoscope_reader/master/Blog/ruby_cli_image_4.png)

Here's where things start to get interesting.  When I'm coding I prefer to have the main files I am working with all open so I can visually trace how each method is working together.  We have three files displayed here:
1. *cli.rb* is where all our actionable methods live.  Here we're greeting the user, generating and displaying a list of available astrological signs to choose from, accepting user input and display the user's selected sign, and asking the user if they would like to read another sign's horoscope.
2. *horoscope_scraper.rb* is designated for pulling, or scraping, data from the Horoscope.com website.
3. *horoscope.rb* uses the data pulled from our scraper file to make new objects that the cli file uses to display our data in the user's terminal and allow the user to interact with the data.
These three files work in tandem to grab data, create an from that data object, and display the data.  This act of different files and methods working separately but together is referred to as *Separation of Concerns*.  Every method and file has one job.  It is important to set up our program this way because it not only allows the program to run more effciently, but it also helps in troubleshooting as we start creating larger programs and applications.  Let's dive deeper.

If we type `bin/run` in our terminal, our program kicks off by checking the run file, which as we covered before, gives direction to create a `.new` version of our program.  In order to create a new version we will need to head over to the `CLI` class method, located within the *cli.rb* file, for futher direction.  Upon entering the *cli.rb* file we find the `CLI` class method, so the system knows this is where to go for the next step.  What's next from here?  We hit our `run` method!  Inside this method are a few tasks.  Before we go further, let's define a couple of things:
* *Class Method*:  Our system will start here to figure out if what it's looking for is inside.  So maybe better described as a house and inside the house are doors.  If we run into the house, we'll open a few doors to find the room we're looking for, but we're tidy so we label our doors to make it faster to find the right door.
* *Instance Method*:  Once we find the right door, we go inside the room and inside the room our instance methods are actions that can only happen within the room.

Alright so we've hit the `run` method, which tells us to activate the next few methods:
* Our `greeting` method greets the user and simply puts out our greeting to the screen.
* Our` pull_signs` method  hits up the `HoroscopeScraper` class method within our* horoscopescraper.rb* file and goes inside to the `scrape_signs` method, which accesses our [Horoscope.com](https://www.horoscope.com) website and pulls the astrological signs and dates that correspond with those signs, as well as the link we'll need to remember for later when the user selects which sign's horoscope they want to view.  We hit up our `Horoscope` class within the *horoscope.rb* file to say, "Hey program, instantiate, or generate and save each sign, date, and link as a new object within a hash (a dictionary-like collection of unique words, or keys, and the data, or values, associated with those words) for us to access later."
* Our` display_signs` method goes through each of the objects created above and puts out just the sign and corresponding date to the screen, and associates a number to each sign and date combo.
* Our` main_menu` method asks the user to enter the number that coincides with the sign they would like to view the horoscope for.  Here the user will enter a number, which will be converted to an instance variable, `sign`. `sign` checks all the objects saved in our hash and finds the sign/date/link combo that coincides with that sign.  Then it visits the `HoroscopeScraper` method in our *horoscopescraper.rb* file but this time goes to the `scrape_horoscopes` method and says, "Here's the sign we are looking for, what is the horoscope for this sign?"  The website takes a second look at the website and goes another level deeper to get the day's horoscope associated with that sign, and then puts out the sign's horoscope to the screen.  Ending here and going back to our `main_menu` in the `CLI` class, the method continues on to the `choose_another?` method.
* `choose_another?` asks the user if they would like to view another sign's horoscope.  The user can either enter Y (or y, since we have programmed all entries to convert to lower case for consistency), which will take the user back to the top of the main_menu, or N (or n) to exit out of the program.  If the user enters anything else aside from Y or N (or y or n), the program will let the user know it did not understand the user's input, and again ask the user to enter Y or N.
