I had a hard time finding tutorials on how to set up a Rails and React authentication for one of my projects. I found a video but found that there weren't many complete readable guides on how to do this until I stumbled upon this video. Here's the first of the series:

> https://www.youtube.com/watch?v=z18zLCAg7UU&list=PLgYiyoyNPrv_yNp5Pzsx0A3gQ8-tfg66j

Following the instructions in this video, I found how to set up user authentication. But I did run into some troubles along the way. I just want to document some struggles that I went through and what I did to set up my program. Most of the information on here would be from the video, but I will do my best to try to incorporate other information I've read from other sources too. 

## Rails Backend

### Create Project Skeleton

```
rails new authentication --database=postgresql
```

The database flag is to tell our application that we would be using PostgreSQL as our database. This is the first time that I have used this flag. I have only used the API flag. Rails does have an API only application but if we do that, we won't be able to use sessions without adding more dependencies back in. So we are generating a regular application but we won't be using any of the views, we are treating it like an API only application. This line will create the skeleton of our project.

### Configure the Database

Once the project skeleton is created, we can now connect our database. In the following file:

> /config/database.yml

Under the development section, make sure to uncomment and configure the username and password to your database. I'm doing this on Windows (not sure how different it is on a Mac), so I had to make sure that my database was running too (pgAdmin 4). Once I configured my database, I create the database by the following line:

```
rails db:create
```

### Install Gems

Once the database has been created, the following gems were installed: bcrypt and rack-cors. Run bundle to download dependencies.

```
bundle install
```

### Configure cors.rb

After installing the gems, I didn't have a cors.rb as one of my files so I had to create the following file:

> /config/initializers/cors.rb

In this file, CORS give you the ability to whitelist certain domains. Because we will be passing secure cookies back and forth between frontend and backend application, we need to be able to use a tool called credentials. If you're going to use crendentials and work with sessions, you have to implement a tool called CORS and implement specific sets of rules for how you're going to communicate. These rules are defined in this initializer.

```

Rails.application.config.middleware.insert_before 0, Rack::Cors do
    allow do
        origins "http://localhost:3000"
        resource "*", headers: :any, methods: [:get, :post, :put, :patch, :delete, :options, :head], credentials: true
    end

    allow do
        origins "https://..."
        resource "*", headers: :any, methods: [:get, :post, :put, :patch, :delete, :options, :head], credentials: true
    end
end

```

We're inserting a level of middleware and we're using the CORS module to do it, so at the very top of the chain, we want to establish these rules. So all the rules that we place inside here are intercepted by the Rails config. If an app tries to communicate with our system thats not authorized to do so, we don't want to give them any access to this application. 

Origin is going to change depending on what frontend application that we are working with and what port it runs on. Resources that are allowed, so we want to allow all resources (*) and for the headers, allow any. The list of methods that are allowed, HTTP methods that are allowed. So frontend application can use GET, POST, PUT, PATCH, DELETE, OPTIONS, HEAD.

Credentials have to be set up to true. This is what is going to allow us to pass headers and cookies back and forth from the frontend app to the backend app. If this is not here, it will not work. 

The second allow block is just a placeholder. So not only do we have localhost, we need to have the domain that we will be pushing our app to. Our app will be on a server/domain so we need to also allow it here. This is our production server.

### Configure session_store.rb

Along with cors.rb, I also had to create another file:

> /config/initializers/session_store.rb

The session store is where we define what the cookie is going to be structured like. 

```

if Rails.env == 'production'
    Rails.application.config.session_store :cookie_store, key: "_skincare", domain: "skincare.com"
else
    Rails.application.config.session_store :cookie_store, key: "_skincare"
end

```

For sessions, we are going to use cookies, that takes in a few arguments: key. Key is going to be the name of the session cookie. It starts with an underscore and is just a naming convention. We also have to define the domain which is whatever our domain is hosted on.

We need an if/else statement in order to have this work in production and local development environment. We need to make this initializer dynamic based on the environment. 

### Migration and Model

Now it's time to create the User migration table and model!

```
rails g model User email password_digest
```

By entering the above into the terminal, this creates a migration table with an email and password attribute. After creating our migration and model, lets jump into our User model.

```
class User < ApplicationRecord
    has_secure_password

    validates_presence_of :email
    validates_uniqueness_of :email
end
```

Inside, we have a has_secure_password method that is given to us by bcrypt, and this tells the user model that the password_digest field needs to be encrypted. We also add validations to the User model that validates the presence and uniqueness of the email.

### Sessions Controller

In our sessions controller, we have our create action. This is going to be a POST request, when frontend app hits the API, it's going to make a POST request to create a session.

```
class SessionsController < ApplicationController
    include CurrentUserConcern

    def create
        user = User.find_by(email: params['user']['email']).try(:authenticate, params['user']['password'])

        if user
            session[:user_id] = user.id
            render json: {
                status: :created,
                logged_in: true,
                user: user
            }
        else
            render json: {status: 401}
        end
    end

    def logged_in
        if @current_user
            render json: {
                logged_in: true,
                user: @current_user
            }
        else
            render json: {
                logged_in: false
            }
        end
    end

    def logged_out
        reset_session
        render json: {status: 200, logged_out: true}
    end
end
```

So if the user email exists and the password matches, store that in the user variable. If user exists, create a session cookie and render some json. Else if the user does not exist, return a 401 code, unauthorized code. 

For our login method, we also want to add an concern. So our logged_in is going to see if our current_user is available. So now we can just include the CurrentUserConcern module.

For the logout method, we just say reset the session and render a json response.

> controllers/concerns/current_user_concern.rb

```
module CurrentUserConcern
    extend ActiveSupport::Concern

    included do
        before_action :set_current_user
    end

    def set_current_user
        if session[:user_id]
            @current_user = User.find(session[:user_id])
        end
    end
end
```

We are also going to build out a Registrations Controller.

In Application Controller, we also want to add the skip_before_action. Rails has a set of rules whenever we are trying to communicate with a route. One of the rules is that it uses a CSRF token, it is generated through our secret key value and checks to make sure that the User who is typing into the Rails form is the actual user. However, with our API, all of that logic happens in a completely different app which is why we need to skip it here. 

```
class ApplicationController < ActionController::Base
    skip_before_action :verify_authenticity_token
end
```

With all of these set up, we have our backend authentication app.