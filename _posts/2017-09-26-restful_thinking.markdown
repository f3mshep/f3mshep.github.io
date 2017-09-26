---
layout: post
title:  "RESTful Thinking"
date:   2017-09-26 16:26:17 +0000
---


REST is a convention of naming routes in a web application that is resource focused. If you are new to web development, or programming in general, this statement may seem a little obtuse. What this means is that a URL written using REST conventions is focused on the noun, or the resource, in the same way that object oriented programming is focused on treating all data (even functions!) as objects, or nouns in this metaphor. REST conventions are not the only way to write web application routes, but they are some of the most common.

So what does all this mean for the web developer and her trusty controller? What would a RESTful URL look like to access a specific blog post?

cutekitties.com/posts/7

A human looking at this URL can tell that we most likely want to do *something* with the post being accessed, but what exactly? 

The other piece to this puzzle is the HTTP method being used in the application's controller. HTTP has 4 different methods:

* GET
* POST
* DELETE
* PUT

These methods represent the requests that a client's web browser can make to the server that is hosting the content of the web application. GET is a request from the client browser to the server to get the information from the server and show it on the client browser. POST represents a request from the client to send information to the server PC. DELETE requests send instructions from the client PC to the server to remove the specified resource. PUT (using Sinatra's MiddleWare, we see this as PATCH) is a request to update the specified resource with new content. DELETE and PUT are a little tricky since by default, web browsers only know how to make GET and POST requests. In the Sinatra framework, we get around this by including hidden forms associated with delete or edit buttons that tell the controller to interpret the following POST request as a PATCH or DELETE request instead.

Therefore, our blogger would need to write the following (simplified code) in her controller to make this route accessible:

```
GET '/posts/:id' do
    @post = Post.find(params[:id])
   erb :show
end
```

This code snippet tells the controller to catch any GET request with cutekitties.com/posts/id_number (for example cutekittie.com/posts/42) and introspect the request to find the id number of the post, then render the show post page with the post's content. 



