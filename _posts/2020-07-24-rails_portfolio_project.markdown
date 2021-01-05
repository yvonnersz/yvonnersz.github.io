---
layout: post
title:      "Rails Portfolio Project"
date:       2020-07-24 12:45:32 +0000
permalink:  rails_portfolio_project
---

Hello again! This will be the third project that I have completed. Out of all the projects, this one by far has been the most difficult. I think it has a lot to do with everything that's been going on in the world that I find it hard to be able to just focus on anything. Despite having so many drawbacks, I still learned a lot from coding this application. There were many interesting tools that I discovered that made the process of coding this application more fun! Some of my favorites are the app name and dummy text generator.

Now without further ado, lets begin.

## Project Requirements
1. Use the Ruby on Rails framework.
2. Include at least one has_many, at least one belongs_to, and at least two has_many :through relationships. Include a many-to-many relationship implemented with has_many :through associations. The join table must include a user-submittable attribute — that is to say, some attribute other than its foreign keys that can be submitted by the app's user
3. Your models must include reasonable validations for the simple attributes. You don't need to add every possible validation or duplicates, such as presence and a minimum length, but the models should defend against invalid data.
4. You must include at least one class level ActiveRecord scope method. a. Your scope method must be chainable, meaning that you must use ActiveRecord Query methods within it (such as .where and .order) rather than native ruby methods (such as #find_all or #sort).
5. Your application must provide standard user authentication, including signup, login, logout, and passwords.
6. Your authentication system must also allow login from some other service. Facebook, Twitter, Foursquare, Github.
7. You must include and make use of a nested resource with the appropriate RESTful URLs.
8. Your forms should correctly display validation errors.
9. Your application must be, within reason, a DRY (Do-Not-Repeat-Yourself) rails app.
10. Do not use scaffolding to build your project. Your goal here is to learn. Scaffold is a way to get up and running quickly, but learning a lot is not one of the benefits of scaffolding.

## Planning
This project was inspired by my recent plant enthusiasm that I just picked up due to the global pandemic. Due to poor planning, I found that the focus of my app just kept constantly changing as I coded out my project, which lead me to rewrite a great deal of code. In the future, I would like to spend more time during the planning phase just to have a clear, well thought-out user story before actually typing in any code for the project.

In the end, this was what the user story came out to be:

> A User can create Stores to sell their Indoor Plants to other users. Once a store has been set up, the user will have the ability to look at their store statistics, such as: income, amount of plants sold, and best-selling plant. The user will also have the option to buy plants from other stores by loading their account balance with cash. Once a plant is bought, that plant will be added to the user's plant collection. 

## Project Skeleton
With Sinatra, the project skeleton was created by adding and installing the gem, Corneal. That is not necessary with Rails; in fact, it's much less complicated. With just a built-in one-line command, Rails will create the base skeleton of the project.

```
>> rails new Plant
```

After the creation of the base skeleton, I have a personal preference to work in the following order:
1. Migration Tables
2. Models and Associations
3. Seed Data
4. Add Routes
5. Controllers
6. Views

## Migration Tables and Models
I am a visual learner so when it comes to creating multiple migration tables and their associated models, I prefer to draw them out instead of typing them in list form. Below is the drawing of the four models and their relationship associations. This is a useful drawing that I like to quickly look at and reference to if needed.

![](http://ibb.co/6BJ78jK)

To save some time, I used the model generator to create the migration tables, models, and associated attributes simultaneously. One useful tip that I learned through this process is that the Rails generator automatically assumes the attribute is a string unless stated otherwise. So the first code snippet is actually equivalent to the second code snippet. The only thing that differs is the amount of keystrokes!

```
>> rails g model User email:string password_digest:string uid:string name:string cash:integer
```

```
>> rails g model User email password_digest uid name cash:integer
```

After the models are created, the relationship associations (belongs_to, has_many) were then created in the model. This was done easily by just referencing the drawing made during the planning phase. One thing that I tend to forget is which migration table gets the foreign key. As of now, I don't really have a good method of trying to remember this other than just memorizing it, but it is the child table that posseses the foreign key.

Validations were also added to the models to prevent bad data from persisting to the database. Uniqueness was checked for user emails and store names. Numbers greater than one were checked for user cash and plant price.

## Seed Data
This portion of the project had me scratching my head for a long time. After creating some dummy data in my seed file, I dropped into the console sandbox to check if my association relationships were working correctly. For some unbeknownst reason, some of my data were not persisting to the database. After trying and failing many times, I found a helpful method on the web to find out why the data was not persisting.

```
>> user = User.new
>> user.errors.any?
>> user.errors.messages
```

If the data is giving any errors, the code above would return a message as to why the data will not persist. Seems pretty straightforward now but hey, hindsight is 20/20... After finding out what was causing the data not to persist, I was able to fix the data and get the association relationships working.

## Routes
Custom and nested routes were set up to prepare for the next section of coding. The routes had the following format:

```
  get '/login' => 'sessions#new'
  post '/login' => 'sessions#create'
```

```
  resources :users, except: [:index] do
    resources :stores, only: [:index, :show, :new, :create]
  end
```

## Controllers and Views
The next step is to create the controllers and the associated view pages. Just due to preference, I did not use the resource or controller generator to create the needed files. The files were created manually. I personally like doing this better because:

(1) I feel like I'm more in control of the files that are created 
(2) I don't have to delete any unnecessary files, and
(3) I feel like this solidifies my understanding of the app. 

Similar to the previous Sinatra project, there really isn't anything new going on in the controllers and the views. As usual, the logic in the controllers are limited and more focused on managing data flow; and the views are there to just simply render whatever is sent from the database.

One part that is unique to this project, however, is the ability to sign up and login via FaceBook. This was done by using the OmniAuth and dotenv-rails gem. The instructions were a bit outdated but after tinkering with the FaceBook developer tools, I was able to get it to work. And since this app requires user login, helper methods were created to expose the current user so that the methods could be used throughout the whole app.

## Scope Methods
> A User can create Stores to sell their Indoor Plants to other users. Once a store has been set up, the user will have the ability to look at their store statistics, such as: income, **amount of plants sold**, and **best-selling plant**. The user will also have the option to **buy** plants from other stores by loading their account balance with cash. Once a plant is bought, that plant will be added to the user's plant collection. 
> 

Referencing back to the user story, it is clear that three instance methods will need to be built: buy, plants_sold, and best_selling_plant. #buy will be built in the IndoorPlant model and #plants_sold and #best_selling_plant will be built in the Store model. With a clear idea of what I want the methods to do, it is time to begin coding them!

What helped me tremendously during this coding period is binding.pry. Going from front-end to back-end, I went in calling the method on the instance variable and used pry to fix any issues that came up along the way. With these instance methods built, the user will now be able to check their store's statistics.

Also, for the sake of fulfilling the project requirements, a class method, Store#by_user, was built to filter out stores created by a selected user. 

## Struggles Worth Mentioning
I also wanted to mention some outside struggles that I encountered that were not directly related to the application.

For this project, I wanted to code in an environment other than Learn IDE just to familiarize myself with other coding environments. It took me a couple days to get the hang of using Visual Studio Code but I can say now that I am more comfortable with using it, which I think will be beneficial in the future.

Another troublesome struggle was GitHub! I ran into multiple GitHub issues while coding this application. One issue that I came across was being behind the master branch, which in turn did not allow me to commit any of my new code. There were instances where I lost some code due to not pushing my work correctly. With the combination of using a different coding environment and the GitHub issues that arose was just a nightmare to deal with. But due to this, I did find a couple commands that I think will be useful in the future. 

```
>> git pull
```

 If the current branch is behind the master branch, this command can be used to fetch and download content from a remote repository. This will give you the option to approve all the incoming changes so that you can push and commit your work.
 
 ```
 git reset --hard HEAD^
 ```
 
 This git command allows you to remove the most recent commit. 

## Stretch Goals
And with this, the project requirements have been fulfilled! If time permits, however, I would also like to add the following features to the app:

1. Add another Store attribute, stock, that will allow the owner of the store to input how much of the item they have in stock. If bought, the stock would decrease. If item is out of stock, owner would have the ability to restock.
2. Be able to transfer store income to user's account balance.
3. Instead of having different shops, users will have only one shop but can sell plants in different categories.
4. Not really a feature, but I would like to play with the CSS more.

## Finished Project
If anyone is curious about the application, the finished Rails project can be found at the following link: https://github.com/yvonnersz/Plant.

Until next time, happy coding!


			




