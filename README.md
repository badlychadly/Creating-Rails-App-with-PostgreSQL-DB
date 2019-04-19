# Creating-Rails-App-with-PostgreSQL-DB

As a Developer it's nice to know that the Rails app you plan on making a masterpiece can be launched to Heroku without too much headache. Rails comes with SQLight and works well when you are starting out, but because it runs in memory and uses file on disk it is not intended for production. We will cover the basics of creating a Rails app using PostgreSQL, which is the type of db Heroku uses.

### Rails new
Before you can use PostgreSQL you need to make sure you have it installed. If you still have to install in check out the PostgreSQL [docs](https://www.postgresql.org/) then come back!
Now let's create a new React app by running `rails new app_name --api --database=postgresql -T`. The `--api` flag tells Rails that this is just an API and there is no need for the heft of a full Rails app. The `-T` flag tells rails to not include the out of the box test configuration so that we can include the testing framework of our choice. 

### Configure the DB
The pg gem will need to be added in order to interface with the database. You may need to create a role using `psql` in the terminal, unless you are ok with the default role assigned. Assuming you are in the directory of your new Rails app navigate to config/database.yml. This file is where we will tell the Rails app what database to use. It should resemble this when first opened.
```
default: &default
  adapter: postgresql
  encoding: unicode
  # For details on connection pooling, see Rails configuration guide
  # http://guides.rubyonrails.org/configuring.html#database-pooling
  pool: <%= ENV.fetch("RAILS_MAX_THREADS") { 5 } %>

development:
  <<: *default
  database: app_name_development
```
You may need to set a password option for development settings, but only if the assigned role requires it. When the configurations are ok we can run `rake db/setup` to have Rails create the development db and the test db.


### Set for Migrations
If you followed these steps you should be ready to use the Rails generator for your next steps. The schema.rb file will not exist until you run your first migration. You are now ready to build an amazing Rails app using PostgreSQL!
