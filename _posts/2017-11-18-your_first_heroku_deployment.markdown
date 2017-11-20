---
layout: post
title:      "Your First Heroku Deployment"
date:       2017-11-18 17:39:58 -0500
permalink:  your_first_heroku_deployment
---


After two weeks of hard work, I was very excited to deploy my KetoTonight web application to the web! I wanted the world to be able to see my wondrous creation!  Heroku is THE web application hosting platform today, so it seemed like a great place to start. Deploying my SQlite3 app should be a breeze, right?

I quickly learned this is easier said than done. 

Let me back up: Heroku is a cloud platform as a service that hosts web applications. It integrates with git for rapid deployment. What does this mean for you, the trusty software engineer? You get to worry about just the web app you are writing, and not the messy inner-machinations of deploying to a server. This ease of use comes at a cost: You must subscribe to a series of conventions. One of these is that your database uses Postgresql.

Postgresql operates a little differently than SQlite3. SQlite3 runs in memory, and stores the database files on hard drive storage. Postgresql runs on a server, which happens to mesh better with Heroku’s database stack.

At this point, there is a great chance you do not have Postgres installed on your computer.  Since Postgres is server based, it  will require a little more configuration than just simply installing it like SQlite3. Not to fear, I will take you through the whole process! I am making the assumption that you are using an equivalent to Ubuntu 14.04 or greater. Instructions should be similar on a Mac, but not identical. The greatest deviation will be how you actually install Postgres. 

First, make sure you actually have Postgres installed!

```
sudo apt-get update
sudo apt-get install postgresql postgresql-contrib
```

**A quick note on roles: **

Postgres only let authorized accounts view and make changes to a database. These accounts are called roles. For ease of configuration, I recommend that give your role the same name as your account you use to log on to your computer. When you install Postgres, it will create a default Postgress role called (imaginatively) postgres. We will use this default role to set up a new role that you can use.

With that in mind, enter the following command into your terminal

`sudo -i -u postgres`

This will start a session with the default account. 

The following command will start an interactive process to create a new account. 

`createuser --interactive`

When prompted, enter the account name you use to log onto your computer, and hit the 'y' key to give the new role super user access.

Done with Postgres configuration! Give yourself a high five.

Now it is time to convert your application to use Postgres. 

It is probably a good idea to make a new git branch for Heroku deployment. This step is not necessary, but is recommended! Push any changes, then enter the following (replacing “heroku_branch" with whatever you want to call your new branch)

`git checkout -b heroku_branch`

Now,  remove the sqlite3 gem from your applications gemfile, and replace it with the postgres gemfile

`gem ‘sqlite3’`

to

`gem ‘pg’`

While you are in the gemfile, add a line at the end with your Ruby version. You don't *have* to specify a Ruby version, but Heroku will give you a warning without a specified version.

`ruby “2.3.1”`

Great! Now, run

`bundle install`

to install the new gem, and remove sqlite3 from your gemfile.lock

Open up your database.yml file in the config folder. We are changing the database adapter from sqlite3 to postgresql.

```
#config/database.yml

adapter: sqlite3
```
 
Change all instances to 

`adapter: postgresql`

Now, run 

```
rake db:create
rake db:migrate
```

You can also create a Procfile in the root of your web app. This is optional. If you don’t you will get a small warning during the deployment process. Follow the instructions here if you are interested: [Procfile Setup](https://devcenter.heroku.com/articles/procfile)

This is important: PUSH YOUR CHANGES TO GITHUB. If you don’t , you will get an error informing you that there is a reference to sqlite3 in your gemfile.

Sign up for a Heroku account and install their software using the instructions here:
[Heroku CLI setup](https://devcenter.heroku.com/articles/heroku-cli)

Time for the moment of truth!

Open a new terminal in the root directory of your web app. Type 

```
heroku create
git push heroku heroku_branch:master
```

or simply 

```
heroku create
git push heroku master 
```

if you did not make a new branch for Heroku.

Wait a moment, and your app should be deployed!

If you get the dreaded sqlite3 error, make sure there are no references to sqlite3 in your gemfile.lock, gemfile, or database.yml files. Some gems depend on sqlite3, they must be removed as well. Also, check to make sure you have pushed your most recent changes! Heroku pushes from your most recent git version.

If you made it this far, congratulations! The world can now see your wonderful new web application.

Shameless plug, check out [KetoTonight](https://stark-harbor-64502.herokuapp.com/.)


