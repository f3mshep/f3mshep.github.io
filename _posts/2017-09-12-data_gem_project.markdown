---
layout: post
title:  "Data Gem Project"
date:   2017-09-12 00:03:03 +0000
---


During the Learn.co curriculum, we have a series of final projects that put a bow on each collection of topics of study. The first project is a command line interface ruby gem that scrapes the web for data. Other than the requirement that we scrape content from the web, the guidelines are not very restrictive.

I find myself at a creative loss of words when I have no restrictions – I find it mentally stimulating to puzzle my way through requirements. My first project was something lurking around in the back of my mind  since I began the course in August.  I eventually turned to the concept of something related to Magic: The Gathering after a conversation with my romantic partner. She suggested I build something related to one of my favourite hobbies.

Magic: The Gathering is a fantasy collectable card game with over 17,000 unique published cards. Its first set of cards was published in 1993. A set is a selection of cards that are designed to be in the same play environment. There have been 84 sets released, with many more planned.

Magic: the Gathering has a thriving economic community based on buying and selling magic cards. Some cards can several thousand dollars, while others can be worth a few pennies. Each card has its own unique set of rules regarding how it can interact with other cards in the game. 

Due to the wide range of cards and prices associated with each card, I thought it would be interesting and useful to build a gem that searches a catalogue of all published cards to display information such as rules text and average market price on individual cards.

My first hurdle I had to clear while designing this gem was choice of website to scrape. I originally planned on using TCGPlayer. I wrote all my tests for my scraper and card classes with this website in mind. To my dismay, the first time I used Nokogiri to scrape data from TCGPlayer I got an HTML document with the class boldy declaring “NO-ROBOTS.”

Luckily, after some desperate googling, I found a comparable website, Scryfall.com,  that allowed me to search for Magic cards. All was not lost, I simply had to rewrite my rspec tests! I commiserated with a friend who went through a similar issue with his project. If I had one piece of advice to give to other students, please make sure you can scrape your website with Nokogiri before you move beyond the planning phase! 

Once I found a website that worked, I found that programming the scraper class was very zen. Launch IRB, look on the page for the data you want, test your selector statements in IRB, mess around with RegEx expressions on Rubular, rinse and repeat.

Writing the card class which kept track of individual card attributes was a simple affair. I designed it to take in an array of hashes and build a collection of cards with attributes that could be modified.

I had a great 'AHA!' moment while I was demoing a gem to a friend. Originally, my gem would scrape the search page, create an array of URLs and names that was passed to the other scraper method in the scraper class that would scrape each card profile page, and then pass that array of hashses to the card class. This worked decently enough with a small number of hits, but his search yieled 60 results - it took about 45 seconds to build the whole collection of cards! 

I optimized my app by making the scraper class only scrape the card profile page when the corresponding individual card is accessed through the CLI. This cut the initial load time down to a second or two. That was one heck of an optimization!

One other improvement I would like to make for this gem down the road is to have it use Scryfall's API, which is much more reliable than scraping data from a webpage. The trouble with scraping data from a webpage is that you are at the mercy of the website's creator. The way data is structured on the website is subject to change at any time, which can spell trouble for an out of date scraper!

I really enjoyed working on this project. I am proud to have made something that I find useful. I hope other members of the Magic: The Gathering community feel the same way!



