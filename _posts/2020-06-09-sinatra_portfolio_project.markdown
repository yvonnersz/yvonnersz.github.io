---
layout: post
title:      "Sinatra Portfolio Project"
date:       2020-06-09 19:24:46 -0400
permalink:  sinatra_portfolio_project
---

Second project down! It has nearly been three months since I have started coding and I am genuinely impressed by the amount of complex information I have been able to process and understand. Similarly to the first CLI Data Gem Project, Flatiron has many saved video lectures to assist with building the project and I will be eternally grateful for them!

## Project Requirements
1. Build an MVC Sinatra application.
2. Use ActiveRecord with Sinatra.
3. Use multiple models.
4. Use at least one has_many relationship on a User model and one belongs_to relationship on another model.
5. Must have user accounts - users must be able to sign up, sign in, and sign out.
6. Validate uniqueness of user login attribute (username or email).
7. Once logged in, a user must have the ability to create, read, update and destroy the resource that belongs_to user.
8. Ensure that users can edit and delete only their own resources - not resources created by other users.
9. Validate user input so bad data cannot be persisted to the database.

**BONUS:** Display validation failures to user with error messages.

## Step One: Planning

My Sinatra portfolio project was inspired by my previous company. During my time there, we had a warehouse full of chemicals that the team wanted to keep track of so that production wouldn't halt to a stop due to lack of materials. Managing these materials by hand or by Excel every week was nearly impossible for the team. Despite still having downsides of migrating to an online system, the process of managing the raw materials was much more efficient.

Here is the background snippet that was the basis of my Sinatra application:

> As a team lead of a company, you are responsible for keeping track of the physical inventory to make sure your team has enough raw materials to run its process for the day. Instead of having to run back and forth to the warehouse to physically count the inventory, you and the other team leads have decided to keep track of all inventories online! As a team leader/user, you will be able to create, read, update, and delete a selected chemical to accurately reflect the physical inventory for your team.
> 

## Step Two: Project Skeleton

Similar to my last CLI Data Gem application, starting the project skeleton has always been a challenge for me. I fumbled with it for a bit before I found out about the gem, corneal! The 'corneal' gem allows us to quickly generate a Sinatra template with Rails-like simplicity, which saved me the hassle of creating all the necessary file structures to start my application. Corneal also included all the required gems that I would need (except for sinatra-flash) so that I could start coding my application right away.

## Step Three: Migration Table

After drafting my application, I knew that I would have two migration tables: User and RawMaterial.

The User table will have the following attributes: username, password, and raw_material_id; and the RawMaterial table will have the following attributes: chemical, company, lot_number, amount, and user_id.

After creating the tables, the tables were seeded with dummy data to associate the ActiveRecord methods. Dropping into the tux console can confirm that the methods created are working as they should.

## Step Four: Models

Following the migration tables are the class models: User and RawMaterial and they would both inherit from ActiveRecord::Base.

The RawMaterial class is pretty basic and will only contain the following line: `belongs_to :user`.

The User class has a has-many relationship with the RawMaterial class, therefore will contain the following line: `has_many :raw_materials`. The User class will also have an additional line of `has_secure_password`, which is an extra security feature that will encrypt the user's password to prevent account theft. This macro is provided by the 'bcrypt' gem that also allows us to use the method, `authenticate`, to verify the user's password.

## Step Five: Controllers

My Sinatra application had three controllers: ApplicationController, UsersController, and RawMaterialsController. Out of the three controllers, the ApplicationController was the most important. The other controllers are basically just playing a ball game of catch and throw, nothing too exciting.

### ApplicationController

```
class ApplicationController < Sinatra::Base

  configure do
    set :public_folder, 'public'
    set :views, 'app/views'
    enable :sessions
    set :session_secret, "kanban" # An extra security feature.
    register Sinatra::Flash
  end
	
end
```
	
This section of code allows the ApplicationController to inherit from Sinatra::Base, which allows the developer to create routes, render pages, and redirect the user to another page.

The configure block shows Sinatra where the view files are located so that the following lines, such as: `erb :login` could be used. It also enables sessions so that the user can stay logged in. This allows for a greater user experience without having to log in every time the user navigates to a new page.

Sinatra::Flash was added to the configure block to allow for flash messages.

In addition to that, the following helper methods were added to the ApplicationController so they could be used throughout the whole program:

```
	helpers do
	def current_user
		@current_user ||= User.find_by(:id => session[:user_id])
	end

	def logged_in?
		!!current_user
	end
end
```

## Step Six: Editing 'config.ru'

`Rack::MethodOverride` will allow us to send PATCH and DELETE requests. The following three lines after that are important and are needed to run the controllers:

```
use Rack::MethodOverride

run ApplicationController
use UsersController
use RawMaterialsController
```

Without this three lines, the program would error out.

## Issues Encountered

One of the issues I encountered that took a while to debug was related to object-oriented programming. For the raw materials index page, one of my end goals was to allow the browser to view the user who submitted the raw material. To do that, I wrote the following code:

```
<% @raw_materials.each.with_index(1) do |raw_material,index| %>
			<%= index %>. <b><a href="/raw_materials/<%= raw_material.id %>"><%= raw_material.chemical %></a></b>
			from <%= raw_material.company %>
			submitted by <%= raw_material.user.username %></br>
<% end %>
```

But when I tested it on the shotgun server, an error occurred stating that the method 'username' is undefined for nil. When I tested the same code in the tux terminal, however; the method worked and returned to me the user who submitted the raw material... It took a lot of going back and forth to this section of the code until I somehow finally decided to delete the database and schema and remigrate the tables... and it finally worked! How frustrating!

It then finally clicked to me that when I was testing the shotgun server and creating raw materials that I was not persisting that relationship to the database. When I was testing the code in tux, it was actually returning to me the user information through the database seeds but NOT through the submission forms itself. To fix that, the following code was added to the controller:

```
@raw_material = RawMaterial.create(params)
@raw_material.user_id = current_user.id
@raw_material.save
```

## Stretch Goals

If time permits, I would like to eventually add the following features to my web application:

1. Team leads could alter each other's content and regular users would not have that feature.
2. Decrementing or incrementing amounts for raw materials.
3. Possibly have a user showpage and their submitted raw materials.
3. Not really a feature, but I would also like to tinker with the CSS layout.

## Finished Project
If anyone is curious about the application, the finished Sinatra project can be found at the following link: https://github.com/yvonnersz/kanban.

Until next time, happy coding!
			


