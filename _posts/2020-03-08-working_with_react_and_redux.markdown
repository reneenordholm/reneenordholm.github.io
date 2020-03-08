---
layout: post
title:      "Working with React and Redux"
date:       2020-03-08 05:19:47 +0000
permalink:  working_with_react_and_redux
---


Finally, I've arrived at the moment I've spent 10 months working towards: my capstone project for the Flatiron program!  Over the past few weeks we dived deep into the React and Redux flow, and for our final project our class was instructed to create an application that utlizes a Rails API backend and React with Redux frontend.  We also needed to utilize the Thunk middleware to manage the asynchronous  logic that interacts with the Redux store.

After a few days of deliberation, I decided to create an application that presents a cat image to the user with an option to 'like' or 'dislike' the cat.  After a 'like' or 'dislike' button is clicked, a new cat is presented to the user.  The votes are tallied and an option is presented to view the highest and lowest rated cats.

![](https://raw.githubusercontent.com/reneenordholm/top-meow/master/frontend/public/blog/project-home.png)

Understanding the React and Redux flow was difficult for me at first, but after watching the video series from [The Net Ninja](https://www.youtube.com/channel/UCW5YeuERMmlnqo4oq8vwUpg) and also  [Annabel Wilmerding's](https://github.com/Awilmerding1) complete build out of an [Expense Tracker](https://www.youtube.com/playlist?list=PL4DoqEkMq3aiGtvPSJWK7uY-4ShmAH-So) application, I felt pretty good about taking next steps to plan and start building my own application!

To begin, I drafted an initial plan of my backend and frontend.  Once I actually started building the application, a few details changed or rearranged, but I do like to start of with a general vision as it makes the startup process much easier.

![](https://raw.githubusercontent.com/reneenordholm/top-meow/master/frontend/public/blog/project-layout.png)

Next, I setup the initial Rails API in a backend folder and utilized create-react-app to create the intiial React app in a separate frontend folder. I prefer to keep both of these folders together under the master application folder, asI feel it looks neater.  After setting up these the initial apps and folders, I created my [git repo](https://github.com/reneenordholm/top-meow), and pushed those folders to the master branch.  

It was time to start building!  I dived into the backend of the application first, setting up and testing the database, creating the controller (ensuring it was CRUD friendly and followed the Rails MVC architypal patten), and setting up the routes.  I wanted to keep this application simple so there is only one controller.  With this in mind the backend was relatively simple to set up and I only implemented the index and create controller methods.

The biggest thing I needed to note here is when a new cat was saved to the database.  Since I was using a third-party API, the parameters coming in weren't coming in from a form I set up and have control over, so the create method receives the img_id parameter (rather than the database-generated id) as cats/:id.  If a cat already exists in the database by the img_id it will add or remove a like from that cat, if that img_id doesn't exists, it will create a new cat.

```
class CatsController < ApplicationController
    def index
        cats = Cat.all
        render json: cats.to_json(:except => [:created_at, :updated_at])
    end

    def create
        cat = Cat.find_by(img_id: params[:img_id])
        
        if cat != nil
            cat.likes = cat.likes + params[:likes]
            cat.update(cat_params)
            cat.save

            render json: cat.to_json(:except => [:created_at, :updated_at])
        else
            Cat.create(cat_params)
        end
    end

    private

    def cat_params
        params.require(:cat).permit(:img_id, :url, :likes)
    end
end
```

After running through a few tests through the Rails console, I felt comfortable moving forward to build out the frontend of the application.

To setup the React frontend, I started off by installing the dependencies I new I would need to incorporate (react-redux, redux, react-router-dom, and react-thunk).  I also did an intiial fetch test, synchronously, just to make sure my frontend and backend were chatting with each other appropriately.  During my intiial application planning process I found a simple CSS template from [W3 Schools](https://www.w3schools.com/w3css/w3css_templates.asp), so I went ahead and added that file to my application.

With my synchronous fetch still in tact and loading up a few cats I manually entered into the database, I began by setting up the main Cat container and CatCard component.  The Cat container renders all the cats from the database, interates through each of them, and sends the attributes down to the CatCard component, which is a functional component that does not need to maintain state, as it's only job is to present the cat to the user.

Originally I was fetching a new cat from a third-party API (the [Cat API](https://thecatapi.com/)), but quickly realized a user would most likely never see the same cat again, which would make rendering the top and lowest liked cat later on a bit difficult asmy databse would be full of new cats having only one or two likes per cat.  At this point, once I had 25 cats loaded in my database, I switched the initial fetch over from the third-party API to my own database. Here is where I setup Redux and incorporated the Thunk middleware.

The flow goes like this...

1. Cat container loads all cats from database on page load, and renders one cat.  The Redux store is initialized with all the cats.  The single cat's attributes are sent down via props to the CatCard component.
2. The CatCard component renders the cat as well as the 'like/dislike' buttons via the CatLikes component.  
3. The CatLikes component is a class with an intial local empty state that represents the attributes to be received upon click of the like or dislike button.  
4. When the like or dislike button is clicked, the local state is updated.  When the local state receives an update it dispatches a post request to the databse updating the like count of the cat in the database, and also updates the Redux store's catalog of all the cats.
5. After this update happens, a method is triggered (received as props from the Cat container) that renders the next cat on the screen.
6. We go back to the beginning!

Follow the flow for yourself on my [git repo](https://github.com/reneenordholm/top-meow).

Though there were many tough concepts to learn through building this application, I appreciate the challenge and am happy with the result!  The appilcation accomplishes everything I intended it to.  I have enjoyed working with React and really enjoy the compartmentalization aspect it brings.  Working with Redux seamlessly incorporates another layer to the separation of concerns concept. and Thunk as a middleware made my fetch calls much easier to work with.  Having built with both Vanilla JS and now with React/Redux/Thunk, I appreciate how these tools allow us as developers to accomplish more with less code.  

For your viewing pleasure, [here is a frontend demo](https://youtu.be/CdCas3iFqxM) of Top Meow!

And that's a wrap. (:
