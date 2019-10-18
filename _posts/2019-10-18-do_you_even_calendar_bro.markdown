---
layout: post
title:      "Do you even calendar, bro? "
date:       2019-10-18 23:44:20 +0000
permalink:  do_you_even_calendar_bro
---


As part of the Flatiron curriculum, we take a few weeks to learn a new programming language, then take the training wheels off and build our own application from scratch.  As we wrap up the Ruby on Rails section, I built an appointment scheduling application, focused around salon time management.  I concierge can book an appointment by client, service, and/or stylist.

![](https://raw.githubusercontent.com/reneenordholm/slated/master/app/assets/blog/slated_home.png)

To begin, we can log in or sign up with our email address or via Google Authentication.  The program verifies an email address is not already taken prior to signing up a new user.  I chose the email address as the unique indentifier so that if a concierge first signs up manually, but the later logs in through Google, access will still be granted.  If a concierge signs up through Google, but later wants to log in by their email account, the concierge can simply update their password through the "Edit a Concierge" option, and log in manually via email next time.

![](https://raw.githubusercontent.com/reneenordholm/slated/master/app/assets/blog/slated_dashboard.png)

Upon signing in, we are taken to the appointment dashboard where we see the current week's appointments and also have the option to create a new appointment right from the dashboard.  Validations are set up to avoid double-booking a stylist.  We can click through the weeks previous and ahead to view appointments by week.

Initially, a new user sign up does not include admin functionality.  A non-admin can book and edit an appointment, create a new client, and update their own concierge account.  A concierge with admin functionality can utlize all the non-admin functionality but can also grant admin access to another user, update any concierge account, add/edit a stylist and service.  The images show an 'admin functions' drop down menu, this menu would not be available to non-admin concierges.

Clients and Stylists both utilize nested resources, therefore if we navigate to create an appointment by stylist, the calendar shows only the stylist's appointments and our form to book an appointment populates the stylist we've selected, making it easy to see the stylist's appointments and book an appointment for the selected stylist.

![](https://raw.githubusercontent.com/reneenordholm/slated/master/app/assets/blog/slated_booking.png)

Overall I am happy with how this project turned out!  To think that when I started, I had about 100 items on my to do list and was quite overwhelmed.  Slowly I chisled through the list and though there are still features I would have liked to add, I made it through the project requirements and will tinker a bit more for fun, as time allows.  See below for the front end walkthrough.  Cheers!

<iframe width="560" height="315" src="https://www.youtube.com/embed/6kxpRVOcgq4" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>





