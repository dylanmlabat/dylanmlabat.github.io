---
layout: post
title:      "Using New Tools"
date:       2019-07-21 20:11:48 +0000
permalink:  using_new_tools
---


Building my Rails project was a lot of fun because I spent more time testing out different ways of displaying my data than I did incorporating those methods that I finally decided to use. I set a lot of personal challenges to include quality of life features and couldn't find it in myself to give up on them before spending a few hours researching each option.

One of the last features I implemented was the artist search bar in the application's footer. I knew I wanted users to have that since finding an artist took so many clicks otherwise, especially compared to other data. However, I ran into a lot of trouble being able to reliably and cleanly find and return each artist, since they exist as a sometimes duplicated string attribute of each Album, rather than being unique objects. In a larger scale project I would have changed that, but I didn't have the time to expand that here so late just for my own peace of mind.

I tried a few things, but ran into errors due to the duplicate artist on various Albums. However, after a few hours of researching and testing different ways to look up object attributes, I came across the `group_by` enumerable. This takes takes in an argument of an object attribute and returns a hash that has each unique attribute value as a key whose value is an array of the objects that contain the attribute:

![](https://i.imgur.com/a7euy7T.png)

This finally gave me a reliable way to iterate over my unique album artists and use those keys to redirect users to the correct artist page. This, however, turned out to not be all that frustrating as compared to returning the notes attribute that I added to Listings earlier on.

I knew that I wanted users to be able to select some number of additional notes (or none) when creating/editing a listing. Because of this, using a `check_box` input seemed like the perfect solution. Implementing that came easily enough, since I had also used them in my Sinatra project, but I quickly ran into an issue when trying to return those values on my Listing show view:

![](https://i.imgur.com/paqAJx9.png)

Hours of researching this gave me countless ways of taking in the check_box inputs and then presenting those on the view page, but no matter what it seemed that Rails would take those string values, put them into an array, and then make that array a string itself. The issue seemed to be caused by me creating string values with my check_box fields, rather than creating the check_box collection from an object's attributes. It wasn't until I stumbled upon a comment on Stack Overflow where someone added `serialize :attribute, JSON` to their model that I was able to correctly return that data in my view. It allowed my project to recognize those notes as individual strings and made them much easier to call on.

Of course, this was another ultimately needless addition to my project when I could have settled for a text field or not bothered to include the attribute. However, it was the self-imposed challenges like these that made me really love the process of creating my project.
