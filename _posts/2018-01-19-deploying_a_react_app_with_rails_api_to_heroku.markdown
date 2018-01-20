---
layout: post
title:      "Deploying a React App with Rails API to Heroku"
date:       2018-01-19 19:11:24 -0500
permalink:  deploying_a_react_app_with_rails_api_to_heroku
---

If you are like me, you are eager to share your web applications with the world! While it is cool to have a local copy running on your computer, you can't exactly send your uncle Dean a link to your application's GitHub page and expect him to compile a copy of your awesome application. Thus, deploying your application to the world wide web is neccessary. Plus, what the heck is the point of a web app if it doesn't live on the web?

For my first React-Redux application, I used this [blog post](https://www.fullstackreact.com/articles/how-to-get-create-react-app-to-work-with-your-rails-api/) to set up a create-react-app with a Rails API.  The post details setting up a Rails backend with the -api argument, installing and configuring the foreman gem,  configuring a procfile, and  aliasing 'rails start' to a development version of the Rails app and a webpack dev server simultaneously.  It is a very well written post, but it ommitted one detail: How to get your app deployed to Heroku! I want this post to fill the gap.

I am going to be making 2 assumptions with this post:

1. You have followed the previously mentioned guide to configure a development version of your application.

2. You are using PostGres as your production database adapter, and not SQlite3. Heroku will throw all kind of errors at you if you        attempt to deploy a Rails application to Heroku with a SQlite3 adapter, which unfortunately is the default database adapter for Rails. If you want more information about changing from SQlite3 to PostGres, check out (my post)[http://alexandrawright.net/your_first_heroku_deployment] on the subject!

Before proceeding, I reccomend creating a branch of your application, which will make it easy to revert any changes if something goes wrong.  

```
git checkout -b stable_dev_branch
```

This will create a local branch named stable_dev_branch. Change back to your master branch 

```
git checkout master
```

Take a peek at your Gemfile. If your foreman gem is not in the development group, move it there. It is not neccessary on Heroku.

Rename the Procfile in the root of your directory to `Procfile.dev`. Make a new Procfile in the same location, and put the following snippet inside it:

```
web: bundle exec rails s
```

This will tell the Heroku to start a Rails server when the Heroku dyno starts. For those who are wondering,  a dyno is a miniature Linux virtual machine that can collaberate with other dynos to act as a web server. The more dynos handling an application, the better the performance of the application. If your application has many concurrent users, more dynos will be added on an ad hoc basis.

Now navigate to lib/tasks and open the start.rake file in the text editor of your choice. Replace the rake task with the following:

```
namespace :start do
  task :development do
    exec 'foreman start -f Procfile.dev'
  end

desc 'Start development server'
task :start => 'start:development'
```

This will make Foreman use your old Procfile, while leaving the other Procfile entact for Heroku to use. You will still be able to run the development branch on your computer with rails start!

Go back to the root of your rails application, (not your client folder!) and make a new `package.json`. This file will be ran whenever Heroku builds a production version of your application, which is every time you deploy to Heroku. Inside this new `package.json` file, include the following:

```
{
  "name": "YOUR_APP_NAME_HERE",
  "engines": {
    "node": "6.3.1"
  },
  "scripts": {
    "build": "cd client && npm install && npm run build && cd ..",
    "deploy": "cp -a client/build/. public/",
    "postinstall": "npm run build && npm run deploy && echo 'Client built!'"
  }
}
```

Time to set up Heroku!

If you don't have Heroku installed, take a minute to install the [Heroku CLI](https://devcenter.heroku.com/articles/heroku-cli).

Righto. To make a new Heroku app, run:

```
heroku apps: create
```


Now we must configure the buildpacks. Run the following commands in your terminal:

```
heroku buildpacks:add heroku/nodejs --index 1
heroku buildpacks:add heroku/ruby --index 2
```

This tells Heroku to have nodejs to handle building the node packages, and Ruby to install the gems and run rails. Why is this step neccessary? If you don't specifiy a buildpack, Heroku will scan your code, and assign a buildpack based on the first match it finds. The first buildpack in the search tree is Ruby, Heroku will see your code is Ruby, and ignore the rest. Bad things will happen. Setting up the buildpacks like this will allow both processes to be built.

There is just one more thing we need to do get this puppy rolling. Run:

```
heroku config:set NPM_CONFIG_PRODUCTION=false
```

This effectively tells Heroku  to let nodejs handle package dependencies. 

Fantastic! Time to deploy everything to Heroku and let your web app sing its wonderful song to the whole wide world on the internet!!

```
git add .
git commit -m "Heroku time"
git push

git push heroku master
```

This will take a while, since Heroku is building a production version of your application. 

While it is building, why don't you play some Sudoku on my [Heroku web app](https://sudoku-now.herokuapp.com/)

Once it completes, give yourself a high five!

<br>

<iframe src="https://giphy.com/embed/BwOU6uH7afefu" width="480" height="366" frameBorder="0" class="giphy-embed" allowFullScreen></iframe><p><a href="https://giphy.com/gifs/tina-fey-high-five-t-BwOU6uH7afefu"></a></p>



