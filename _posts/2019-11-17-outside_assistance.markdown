---
layout: post
title:      "Outside Assistance"
date:       2019-11-17 15:44:31 +0000
permalink:  outside_assistance
---


My final project somehow managed to be the first one that I went into being fairly confident that I knew what I wanted to do. While that should have been a relieving part of the process, my confidence tricked me into skipping some pretty important research and ultimately caused a few setbacks that might have been covered by my normal indecision instead.

Before beginning my project I made sure to confirm the requirements. I knew that I only needed to hook the frontend up to my Rails API backend and that would easily be covered by the user registration and login/logout requests that I would be making. However, since that requirement was already covered, I couldn't shake my desire to allow users access to the external Goodreads API to search and add books to their library from that, rather than spending a day adding enough seed data to satisfy me. Since we had essentially done this with the Giphy API in a previous lab, I continued through my backend setup without worry.

![](https://i.imgur.com/mcHNvHg.png)

Unfortunately, my confidence caused me to fail to consider that perhaps not every external API would offer their data in a format I was familiar with. Preliminary searches about the issue showed me that I was not alone in my expectations and that Goodreads users have requested the API update to include JSON endpoints, rather than only XML, for years. I then had the immediate issue of learning to fetch and parse XML, learn to somehow convert XML to JSON, or abandon my idea entirely.

Needless to say, because I had set up my entire backend database based around a sample Goodreads query response not realizing it was XML and because I was now fully in the midst of my final project, abandoning any part of it seemed like a major blow. Unfortunately, after a more lengthy research period, my tests at converting the XML and the gems that I attempted to integrate still failed. I was able to find example Github projects by people that could manually convert XML, but integrating that much external code and trying to swap out my variables seemed like a project in and of itself.

After finally tossing in the towel on Goodreads, I had to face the fact that I either had to find a new book database API to try and work in, fall back to seed data, or change my project more massively. I researched some options that I did not go with (Open Library) but had learned my lesson to research how and which data I could fetch before modeling my project around it. Thankfully, I stumbled on the Google Books API. I did have to remodel my backend, but it ultimately provided the exact data I had envisioned in a way that was much easier for me to parse and use.

![](https://i.imgur.com/jQycfOs.png)

This provided a valuable lesson for me to not set up my expectations before researching the external elements I plan to use. You certainly wouldn't want to write your actions and reducers before setting up the Redux store after all. It also gave me a necessary reminder that API documentation exists for this exact reason. Thankfully, my changes ultimately ended up letting me fetch and store more data than I used for this project and have allowed me to continue to expand on it.
