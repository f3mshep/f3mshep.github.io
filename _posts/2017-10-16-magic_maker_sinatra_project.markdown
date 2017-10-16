---
layout: post
title:      "Magic Maker: Sinatra Project"
date:       2017-10-16 23:33:35 +0000
permalink:  magic_maker_sinatra_project
---

As I am writing this, I am looking out of the corner of my eye at a Terminal window, which is updating my database at breakneck speed. I have just finished my Sinatra Final Project, and I can't remember the last time I have felt such a sense of accomplishment.

My a similiar domain model as my last project, which was a Magic: the Gathering ruby gem that scraped Scryfall.com, which hosts a powerful search engine that allows users to find any MtG card ever printed. I found it a very interesting project, as each MtG card interacts with the game in a unique way, and there are over 17,000 different cards printed! It was a satisfying challenge to figure out a way to display every card without my code breaking.

I decided to take it a step further with this Project! I built a web application that uses the Sinatra micro-framework. It was a very educational experience, since Sinatra lacks much of the "magic" that makes up the Rails framework. The lack of Rails magic helped me get a strong grasp of concepts such as programming with RESTful routes. The web app, which I dubbed 'Magic Maker' is a social network that allows users to create Magic: the Gathering decks and collaborate with other users. I wanted to really challenge myself, so I taught myself how to integrate an API with a Sinatra framework. As a result, the search feature of my web app is powered by the Scryfall API. The database I mentioned earlier contains every single card stored on the Scryfall API.

Something that I found very useful while programming Magic Maker was the process of breaking down big problems into smaller ones. I wanted to design my application packed with features, which meant I had a fairly daunting task in front of me to get everything working! At times, it was panic inducing to look at the big picture. Focusing on the little things allowed me to progress at a steady rate.

The most annoying thing about this project was that it was the first time I wrote something without using TDD. Unfortunately, it was also the most complex. Every time I changed something, I had to test every function of my app. Near the end of the project, this took a while. I learned that even though writing tests can take time, it pays off in dividends!
