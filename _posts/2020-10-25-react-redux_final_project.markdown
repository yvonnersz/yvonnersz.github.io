---
layout: post
title:      "React-Redux Final Project"
date:       2020-10-25 17:57:50 +0000
permalink:  react-redux_final_project
---

## Project Requirements
1. The code should be written in ES6 as much as possible
2. Use the create-react-app generator to start your project.
3. Your app should have one HTML page to render your react-redux application
4. There should be 5 stateless components
5. There should be 3 routes
6. The Application must make use of react-router and proper RESTful routing
7. Use Redux middleware to respond to and modify state change
8. Make use of async actions and redux-thunk middleware to send data to and receive data from a server
9. Your Rails API should handle the data persistence with a database. 
10. You should be using fetch() within your actions to GET and POST data from your API.
11. Your client-side application should handle the display of data with minimal data manipulation
12. Your application should have some minimal styling.

## Planning
Honestly, for this final project it was hard to find inspiration for what I wanted to build. I decided to just pick from the lesson list to create a mock Reddit newsfeed app. I thought this would be a great idea too, since for the previous projects I came up with my own ideas, so I wanted to see how different it would be to build an original webapp versus a webapp clone.

To my surprise, building a webapp clone is much easier! I think it has to do with that a webapp clone I can physically see what components/models are interacting with each other  (I'm a visual learner!!!) versus something that I would have to imagine. In the future, I think if I were to begin building a webapp from scratch, I should probably look around for some websites to find similarities to how I want my webapp to function, just to make my life easier!

Anyway, here is my very basic user story:

> A User would be able to create a post, leave comments, upvote, downvote, edit, and/or delete content.

## Backend
### Project Skeleton
So like with the previous Javascript project, I began by working on my backend. To create my project skeleton, I used the very simple, one-line command:

```
rails new <app-backend> --api 
```

What this does is that it sets up everything that I would be using a.k.a my project skeleton! The --api flag also lets the app know that it will be an API, and would also prevent unnnecessary extra gems and dependencies to be created. 

### Migrations, Models, Controllers, and Routes
I picked the resource generator to create the migrations, controllers, models, and routes. The nice thing about the resource generator is that it will not create any views, which would be unnecessary for this project since the frontend will be rendering the view.

```
rails g resource <Model> username:string password: string karma:integer --no-test-framework
```

The flag lets the app know that there will be no need to build out specs for the app. And just to make things easier, I also included the attributes into the one-line command just to save a bit of time. Once the line was entered, the migration tables, models, controllers, and routes were automatically created.

In the models, I created the associations. I also added in some validations to make sure that the app was getting the data that it needs. This is to prevent bad data from persisting to the database. To the models, I built some extra methods to upvote and downvote any created post or comment.

For the controllers, I needed to set it up so that the url would look like the following: 

> localhost:3000/api/v1/posts/:id/comments/:id 

The reason for this is that it is just standard convention and it's better to just follow the standard protocols. This tells other developers that the controllers are handling the API and v1 is the version. If there ever is a case in where I do  need a second version, I can just nest it under v2 without deleting anything. This prevents it from affecting any previous versions. Also to the routes file, I would need the namespace convention:

```
Rails.application.routes.draw do

  namespace :api do
    namespace :v1 do
      resources :posts do
        resources :comments
      end
    end
  end
  
end

```

From here, I built out all the CRUD actions for my two models.

### Seed Data
I seeded my app with dummy data and dropped into rails console -s to check that my associations were working as it should. The purpose of the -s flag is to drop into the sandbox mode of the console so that the data that I was working with wouldn't persist to the database.

### Serializers
To have my frontend receive the json data in the format that it needs, I installed the gem 'fast_jsonapi' and created serializers for my models.

### CORS
In the Gemfile, I also uncomment the gem 'rack-cors'. This is so that when the frontend is making requests to the backend, there wouldn't be any issues.

After installing the gem, I also uncomment the following section in the initializers/cors folder: 

```
Rails.application.config.middleware.insert_before 0, Rack::Cors do
  allow do
    origins '*'

    resource '*',
      headers: :any,
      methods: [:get, :post, :put, :patch, :delete, :options, :head]
  end
end
```

### Final Comments about Backend
For this project, building the backend folder was way easier compared to when I first started coding! I think that just means I'm gaining a deeper understanding of how all the different components come together and work.

Another thing to mention is that I commit the backend and frontend folders onto GitHub as two separate repos. This is to remind myself that they're both two separate applications. Also, another benefit to this is that if I ever do want to reuse my backend API for a different project, it would just be easier.

## Frontend
### Project Skeleton
Now time for frontend! So to build the project skeleton for React, the following line was entered into the terminal:

```
sudo npm install -g create-react-app
```

The reason why I had to include the sudo npm install -g was because I couldn't run the simple create-react-app command due to permissions. I searched the internet and this was the solution to get around it. After running the above command, the frontend project skeleton was automatically created for me. From here, I deleted all the unnecessary files that I wouldn't be using and created the necessary folders for my frontend project. They each were nested under /src and the folders are: containers, components, actions, and reducers. 

### Installing Dependencies & Setting Up Redux Store

When using the one-line command, create-react-app, Redux will not be added to the package file automatically. Since I will need Redux for this project, I had to manually set it up and install all the following dependencies as so:  

```
 npm install redux react-redux react-thunk react-router-dom --save
```

The purpose of the --save flag is so that the dependencies will be saved in the package file so that the next time I open the app, I wouldn't have to manually install them again. After installing the dependencies to our package file, they were then imported into our files.

From here, I then set up the redux store and connect it to the browser with the following code snippet:

```
const composeEnhancer = window.__REDUX_DEVTOOLS_EXTENSION_COMPOSE__ || compose;

const store = createStore(postsReducer, composeEnhancer(applyMiddleware(thunk)))

ReactDOM.render(
  <Provider store={store}>
    <Router>
      <App />
    </Router>
  </Provider>,
  document.querySelector('.container-fluid')
);
```

To run the server, npm start was entered into the terminal. One issue that came up during this step was that the server was telling me that I was running on Rails... I eventually was able to figure out that my backend and my frontend were both running on the same port. So to get around this issue, I entered the following into the terminal to tell my React server to run on a different port:

```
PORT=3001 npm start
```

### Containers, Components, Actions, and Reducers

Out of these four, I found reducers to be the hardest and most time-consuming one. What really helped was just console logging every step of the way just to make sure that I was on the correct path. One thing I was stuck on for quite a while was that when I used splice, it mutated the original array and my page wasn't re-rendering despite console.log telling me that the array changed. That's one mistake I wouldn't make again!

### CSS

After getting the logic and views down, I then stylized the page with CSS. To do this, I found Bootstrap to be really helpful. Bootstrap comes with some basic styling templates and the only thing I would have to do is install the dependency and import them into my files. To acquire the basic bootstrap CSS, I would then just have to change the div class to the according documentation.

## Stretch Goals
If time permits, I would also like to implement the following features:
1. User login, logout, registration.
2. User can choose from a dropdown menu of subreddits. 
3. Instead of rendering the actual date, render something along the lines of <Posted 7 hours ago>.
4. More CSS!

## Conclusion
If anyone is curious about the project, it can be found here:

https://github.com/yvonnersz/mock-reddit-backend
https://github.com/yvonnersz/mock-reddit-frontend

It was a long and hard journey but I did it! 







