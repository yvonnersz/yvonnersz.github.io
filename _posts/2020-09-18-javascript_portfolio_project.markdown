---
layout: post
title:      "JavaScript Portfolio Project"
date:       2020-09-18 06:15:13 +0000
permalink:  javascript_portfolio_project
---

## Project Requirements

1. The application must be an HTML, CSS, and JavaScript frontend with a Rails API backend. All interactions between the client and the server must be handled asynchronously (AJAX) and use JSON as the communication format.
2. The JavaScript application must use Object Oriented JavaScript (classes) to encapsulate related data and behavior.
3. The domain model served by the Rails backend must include a resource with at least one has-many relationship. 
4. The backend and frontend must collaborate to demonstrate Client-Server Communication. Your application should have at least 3 AJAX calls, covering at least 2 of Create, Read, Update, and Delete (CRUD). Your client-side JavaScript code must use fetch with the appropriate HTTP verb, and your Rails API should use RESTful conventions.

## Planning
Being so close to the finish line, I was wondering what it would be like after finishing my course. I was reminiscing back to my college days after graduation and remembered applying for numerous jobs. Eventually, the amount of applications were so substantial that keeping track of all of them was a grueling process. It would have been nice back then to have an application that could organize all this information for me. Not only that, but also give me some useful statistics, such as: the amount of companies that I got accepted or rejected from, for example.

As usual, I find the planning phase difficult. Having a rough idea of what I want my application to do versus implementing the application are two very different things. Eventually, this is the user story that I ended up with:
 
> This app is intended to help a student organize all their job applications. The user will fill out a form with the company information and upon submission, will create a card with the submitted details. The user will have the option to leave comments on a company card or edit/delete companies, in case of a mistake. The user will also have the ability to filter out cards by either status or date, or view some basic statistics.

After reading through a couple documents, I found a really interesting method in building my project. With previous projects, I tend to build out my features horizontally. Using the method, however, ended up with me having to change all the underlying layers if my code did not work out. If we can visualize the features as columns and the different layers of stack as rows, then we can minimize the amount of rework that will need to be done. This is building it vertically and is a strategic way to minimize writing any unused code.

The next following sections will be built using the vertical method and will look as so:

1. Migrations
2. Models
3. Seed Data
4. Controller
5. Data Fetching
6. View Logic
7. Styling

## Project Skeleton
The backend and frontend will be separated into two top-level folders. As with previous projects, the backend skeleton can be built with a one-line command. To that one-line command, we will add two flags. The api flag will be used so that Rails will know to set the project as an API and the database flag will be used so that Rails will know to use PostgreSQL as the database. The reason why PostgreSQL is used is so that it is easier to deploy the application on Heroku, which does not support the default database for Rails, SQLite. 

```
rails new Jobplica --api --database=postgresql
```

**Cross Origin Resource Sharing (CORS)**

The gem 'rack-cors' will be uncommented in the Gemfile to allow us to setup CORS in our API. CORS is a security feature that only allows API calls from known origins.

> Let's say your bank is hosted on https://bankofamerica.com. If a clever hacker tried to impersonate you and send a request with an origin of https://couponvirus.org, then ideally, your bank would reject requests from unknown origins such as couponvirus.org and only allow requests from trusted origins or domains like bankofamerica.com

In addition, the following code will be uncommented in config/initializers/cors.rb:

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

Inside the allow block, inserting * into the quotation marks mean we are allowing requests from all origins and are allowing get, post, patch, and delete requests to the API.

For the frontend skeleton, the following folders were created: src and styles. The adapter folder and components folder were created and nested into the src folder. 

## Migrations, Models, and Seeding the Data
As with the previous project, the model generator was used to create the migration tables, models, and associated attributes simultaneously. After the models are created, the relationship associations (belongs_to, has_many) were then created in the model. This was done easily by just referencing the notes taken during the planning phase. The data was then seeded. To make sure that the data was seeded correctly, a server was fired to see the JSON representation of the data. 

## Controllers
The controllers were nested as so:

> controllers\api\v1\companies_controller.rb

```
class Api::V1::CompaniesController < ApplicationController
    def index
        companies = Company.all
        render json: companies, include: :comments
    end
	...
end
```

The reason why the controllers were nested as so is because when you're making a request from another origin, you know that this particular application is an API-only type app. It's only sending data and not rendering any type of use. This is a convention used by companies.

This project is also different from previous projects in that we will be rendering the data in JSON format so no instance variables will need to be used. The include is used so that the JSON representation of the code will have the comments nested under the company.

## Data Fetching
The adapters will communicate to the API and relay the information to frontend. The adapters are the "middleman" and where most of the fetch request methods will be built.

```
class CompaniesAdapter {
    constructor() {
        this.baseUrl = 'http://localhost:3000/api/v1/companies'
    }

    getCompanies() {
        return fetch(this.baseUrl).then(resp => resp.json())
    }

    createCompany(companyObject) {
        const company = companyObject

        return fetch(this.baseUrl, {
            method: 'POST',
            headers: {
                'content-type': 'application/json',
            },
            body: JSON.stringify({company}),
        }).then(resp => resp.json())
    }
		...
end
```
## View Logic and Styling
In index.js, a new instance of App is created and that will kick off the constructor which will then create instances of companies and comments. To those files, this is where most of the view logic will occur. After getting the view logic to work, CSS was applied to structure and style the page.

## Struggles Worth Mentioning
1. **Installing PostgreSQL**
Installing PostgreSQL as the database for this project is definitely easier on a Mac then it is for Windows. I've looked up and tried many different solutions online but I still couldn't get it to work. I then remembered a lesson quite a few modules ago that went into a detailed explanation on installing PostgreSQL. I guess I installed it incorrectly the first time which caused problems later down the road.

2. **Planning and Implementing Features**
Implementing the features of my app was definitely a hard feat. For this project, I spent a longer time planning the features of my app because of past experiences. Despite the longer hours of planning my project however, I still had to alter my original ideas quite a bit. In the future, as I am planning my project, I would have to detail exactly HOW I want these features implemented. 

3. **Implementing Stretch Goals**
I spent too much time trying to implement stretch goals. One feature that I wanted for my project was to implement Google Charts. In the end, however, I had to scrap the idea due to time constraints. The biggest issue with it was that since our app is a single-page application, the chart only is accurate upon a page refresh. And from what I've read, Google Chart's draw method only draws once per page load. I had to default to a statistics table instead which was a lot more doable.

4. **Forgetting the Basics**
Since this project is about putting everything that I've learned up until this point into a single app, I find that I was forgetting the basics. For example, I would update my controller actions but forget to update the resource file to allow for the requests. For frontend, it was creating new files but forgetting to add the script to my index.html.

## Some Useful Tips
Along the way, I have also come across a few useful tips:

```
code . => Opens up directory in new window.
mkdir <folder> => Makes directory. 
touch <filename> => Creates file. 
```

Another useful tip in VSCode was that if I typed the shortcut '!' into index.html, it will automatically create a blank HTML document for me. Very neat shortcut and a great timesaver!

There are also some git commands that I have been using a lot more:

```
git clean -fdx => Cleans up any unsaved files not pushed to GitHub.
git checkout -b <branch-name> => Creates a branch on GitHub.
```

## Stretch Goals
 If time permits, however, I would also like to add the following features to the app:
 
 1. Add Google Charts to view job status statistics.
 2. Add a progress bar to see how much further user needs to achieve before reaching endpoint.
 3. Filter by more dates, such as: today, yesterday, this week, last week, last year, etc.
 4. Customize page layout + edit company card layout to my liking.
 6. Feature to not leave empty comments.
 7. Company status on card should be a dropdown menu, not multiple buttons.
 
## Finished Results
If anyone is curious about the application, the finished project can be found at the following link: https://github.com/yvonnersz/jobplica.

Until next time, happy coding!

