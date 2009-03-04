Models
======

Datamapper
----------

Sequel
------
Require the Sequel gem in your app:

    require 'rubygems'
    require 'sinatra'
    require 'sequel'

Use a simple in-memory DB:

    DB = Sequel.sqlite

Create a table:

    DB.create_table :links do
     primary_key :id
     varchar :title
     varchar :link
    end

Create the Model class:

    class Link < Sequel::Model
    end

Create the route:
   
    get '/' do
     @links = Link.all
     haml :links
    end

ActiveRecord
------------
First require ActiveRecord gem in your app, then give your database connection settings:

    require 'rubygems'
    require 'sinatra'
    require 'activerecord'

    ActiveRecord::Base.establish_connection(
      :adapter => 'sqlite3',
      :dbfile =>  'sinatra_application.sqlite3.db'
    )

Now you can create and use ActiveRecord models just like in Rails (the example assumes you already have a 'posts' table in your database):

    class Post < ActiveRecord::Base
    end
    
    get '/' do
      @posts = Post.all()
      erb :index 
    end
    
This will render ./views/index.html:

    <% for post in @posts %>
      <h1><% post.title %></h1>
    <% end %>
