---
layout: post
title:      "The JavaScript / Rails API Relationship"
date:       2020-01-11 17:53:45 -0500
permalink:  the_javascript_rails_api_relationship
---


Next up on my project tinkerings is a Single Page Application (SPA) that utilizes a JavaScript front end and Rails API backend. For this project I decided to create a resume-type page, since I will start applying for jobs soon. I figured it would be a good idea to consolidate my work history and interests in one cozy spot! Upon passing my Flatiron project review for this project, I plan to upload it to Heroku and use it as a personal marketing tool as I connect with people in the development community. We are getting close to the end here at Flatiron and though a bit nerve-wracking to not know precisely what the future holds, it is an exciting and rewarding time!

Here’s a bit of info about my project.

<center> 
![](https://raw.githubusercontent.com/reneenordholm/reneenordholm.github.io/master/img/01112020-nordholm-blog-1.png)
</center>

* I at first attempted to use Postgres for my database, but was having issues with my computer running it properly, so I switched over to SQLite. I will have to switch back to Postgres before uploading to Heroku, but after spending a day attempting to get Postgres to work I decided it was best to stick to what I have already been using lest waste anymore time.
* I started a new Rails app utilizing the Rails API flag. I then enabled cookies manually so I could still utilize cookies while remaining in a more lightweight framework.
* We use vanilla Javascript that follows the ES6 Class syntax. This was probably the most difficult for me to wrap my head around (getting my classes to talk to each other and their appropriate setup), I admittedly still struggle with the concept bu get it on a more general level. The more I tinker the more it makes sense!
* Getting my frontend and backend setup on GitHub took me a few tries, but I eventually set in and was able to start coding. We are essentially building two applications that sync together, so that initial talk can be confusing. After initial setup of my Rails API, I built out a few test data items in my database so I could have data to render in the browser. I like to make sure my database is functioning properly before going too much further.

```
def index
        trades = Trade.all
        render json: trades.to_json(:except => [:created_at, :updated_at])
    end

    def update
        trade = Trade.find_by(id: params[:id])
        trade.update(trade_params)

        if trade.save
            render json: {messages: "trade saved"}
        else
            render json: {errors: "trade not saved"}
        end
    end
```

The the Rails API is able to render in a JavaScript frontend is that all data retrieved from the database is rendered as JSON, rather than rendering to a page created within the Rails app.

```
[
   {
      "id": 2,
      "trade_type": "about",
      "description": "Self-motivated, entrepreneur with the ability to see the big picture, find needs, develop and revamp processes for more efficient and effective production. Quick learner, organized and able to manage multiple projects simultaneously. Computer savvy with PC and Mac. Competent with Microsoft Office Suite, QuickBooks, Adobe Photoshop, and various calendar and email programs.",
      "img": "https://raw.githubusercontent.com/reneenordholm/spa/master/spa-frontend/assets/about_renee.JPG",
      "title": "About Renee"
},
   {
      "id": 3, 
      "trade_type":"work",
      "description": "Manage a team of 4 for retail/coffee shop. Build relationships with customers and employees in order to maintain positive vibes and friendly work environment, create weekly employee sche....
```

The JSON format is easily read by frontend languages like JavaScript, so by retrieving the data from a reliable backend and rendering it in JSON, we can use the dynamic functionality that JavaScript provides in order to create an interactiv and user-friendly website.

Each item in my database is output as JSON and rendered via JavaScript and CSS.   I have a somewhat hidden login feature that enables me to login and edit each database item from the SPA frontend without having to get into the backend or database manually.  Super convienient!  Once logged in, I can just click on the item I want to update and a custom form pops up.  Login/logout, edits, and the initial item renders are all populated via fetch requests to my database.

<center> 
![](https://raw.githubusercontent.com/reneenordholm/reneenordholm.github.io/master/img/01112020-nordholm-blog-2.png) 
</center>

While simple this application is robust and concise in it's innerworkings and effectly hits all the deliverables this project required.  I am excited to have not only learned this new-to-me programming language, but also excited that I have a product I can show off to family, friends, and most importantly, future job prospects!
