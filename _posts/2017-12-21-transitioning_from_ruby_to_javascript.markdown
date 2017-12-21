---
layout: post
title:      "Transitioning from Ruby to JavaScript"
date:       2017-12-21 19:32:50 +0000
permalink:  transitioning_from_ruby_to_javascript
---


If you are like me, you absolutely love Ruby. It offers a great deal of power hidden behind simple syntax. It gives programmers the freedom to solve a problem in multiple ways with all the slick tools in its belt.  It is often said that learning a language changes the way we think. Following this logic, Ruby’s elegant style promotes elegant code that is easy to read.

If you are also like me, the transition to JavaScript was a little… rough. Compared to Ruby, functional JavaScript code looks like a mess of spaghetti, both visually and logically. What are all those curly things doing??? Is that function returning a function!? Why is there is no built in way to numerically sort arrays, even though sort() sorts arrays of strings right out of the box?? Truth be told, I missed Ruby more than a little once I entered JavaScript land. After working with JavaScript, I have decided JavaScript is great in its own weird way too! If I can change my mind, I bet you can too.

JavaScript was born in 1995. Its prototype was written in 10 days, and was named JavaScript as a marketing ploy based off Java’s popularity. JavaScript caught on as the defacto language of the web, and has been maintained and updated since then. 

What makes JavaScript special is its ability to manipulate the document object model (DOM), or essentially what you see when you go to a website. The world wide web is a huge place, by 2020 there is expected to be 50 billion devices connected to the internet. Web browsers all need to meet the same standards so that JavaScript works on them as uniformly as possible. JavaScript has a huge burden on its back. After nearly 25 years javascript is still able to do its job, a fact that I find remarkable.

The core philosophy of JavaScript is freedom… at any cost! It must be able to adapt to any situation, even Internet Explorer 6. It is extremely lenient in what it allows, and it actively tries to make sense of anything that is thrown at it. Want to add an integer and string? Sure! Want to call *console.log()* with 7 arguments? Why the heck not!? Of course, this freedom can lead to interesting situations. 
```
'b' + 'a' + + 'a' + 'a'
//banNaNa
```
JavaScript dutifully tries to make sense of this string concatenation. It sees + + and thinks you must be trying to convert that ‘a’ into a number! It tries to make an integer out of ‘a’, fails, and kindly informs you that ‘a’ is not a number. Then it keeps chugging and concatenates the whole thing, returning ‘’BaNaNa”. This is one of my favourite examples from WTFJS, a GitHub repo that contains examples of JavaScript acting goofy. If you need to cheer up after a long day of debugging JavaScript code, I recommend checking it out. [WTF JS]( https://github.com/denysdovhan/wtfjs)

One of JavaScript’s biggest strengths is that it treats functions as first class objects. This means that a JavaScript function can build another JavaScript function, that you can use at a later time, store in a variable or a data structure, or simply return the newly minted function as the return value of the function that created it. You can see this principle in action when you type in the name of a function into a browser console. 
Let’s define a function to check this out:

```
function sayHi(){
	console.log("hi")
}
```
If you type in:
```
sayHi
```
Your console will return:

```
ƒ sayHi(){
	console.log("hi")
}
```
Why? Using Ruby vernacular, you have typed in the key to a hash, and it is returning the value! (In JavaScript, hashes are more or less referred to as objects) When you add ‘()’ to the end of the key, you are telling JavaScript you want to run the value that is returned!

For a more practical example of functions as first class objects, check out *bind()*.

```
myFunc.bind(thisValue, args)
```

 Bind is a function that is pointed at another function, and takes in at least 1 argument. It returns a new function based off the target function Bind is called on. The first argument is what you want to set the new functions this value to (which is similar to Ruby’s self). The rest of the arguments (as many as you want or as little as you want, including zero) you call bind with will be passed in as the first arguments to the new function. 

One of the most useful ways to utilize bind() is to use it to borrow an instance method from a different class and use it as an instance method in new class. You can’t do this in Ruby without some serious hacking, but it is very simple in JavaScript because of how it treats functions.

When learning a new language, it is important to keep in mind the lessons you have previously learned about programming, but it is equally important that you play to the new language’s strengths. Keeping this in mind will help you learn new programming languages quickly and efficiently. Ruby will always have a special place in my heart as my first love, but that doesn’t mean there is no room for other languages in my heart as well.

 




