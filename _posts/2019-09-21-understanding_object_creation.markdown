---
layout: post
title:      "Understanding Object Creation"
date:       2019-09-21 20:13:54 +0000
permalink:  understanding_object_creation
---

I was feeling pretty confident by the time I reached the last requirement of my Rails with Javascript Portfolio Project. The bulk of my project already existed and the previous Javascript updates went pretty smoothly, aside from some complexities I added to the index feature when I first began. I had watched a few Learn Instruct tutorials and generating and posting the form looked simple enough, so I decided to also try to spice this one up a bit.

My first idea was to have a secondary form popup on the new listing creation page that would allow users to create a new album to then choose from the dropdown without having to navigate to another page and back instead. The javascript/css for creating, opening, and closing the popup came easily enough. However, I ran into major issues when submitting the AJAX post request from the form because it would attempt to post the listing form instead. Naming each of the forms did not seem to have an impact. If it was added into a popup the form couldn't be found when inspecting the DOM. Ultimately, I wasn't able to figure out a workaround for this and, feeling crunched for time, decided to move my form requirement to the artist pages so that users could add new albums and see them append to the album list on the DOM without a full page redirect.

What I did not expect was to run into a similar problem. Again, adding the form came easily enough and I was able to ensure that my code was submitting the AJAX post request with the correct form and parameters this time. However, I again ran into posting issues, despite following the standard procedures I had seen in the guides I watched:

![](https://i.imgur.com/ibCwH5h.png)

Some brief research into the problem gave me a very simple solution: just remove the `.require(:album)` portion of my album params. And that did work! To my chagrin, though, going back and testing my original album creation form no longer worked. I didn't want to simply remove this previous form. First, it was already a part of my project, and going backward to fulfill this other requirement seemed cheap. Secondly, I still wanted the original form to function as it did. If there was not already an album by a certain artist then there would be no artist page to add albums into, effectively limiting my app to the seed data included or forcing users to add albums at that level, which obviously wouldn't be accessible in a real-world scenario.

![](https://i.imgur.com/FxIxRwb.png)

Eventually, I came to understand how these forms were submitting differently, the original as a value hash to the album key and the AJAX post as a set of JSON form parameters that filter into a hash during the post process. Rather than rely on `$(this).serialize()` to set my parameters for me, I had to emulate that hash format myself and pull from `this` that way:

```
var valuehash = {
          artist: this[0].value,
          title: this[1].value,
          release_year: this[2].value,
          genre: this[3].value
        }
var album = {album: valuehash}
var posting = $.post('/albums', album)
```

It was once I understood this that I was also able to go back and refactor the hash, automatically pulling the artist value from the h1 on the DOM so that users would not accidentally create new, separate artists if a typo was present. This was ultimately my favorite part of the project, despite my struggles with the code at first. I am excited now to go back and figure out the first idea that I abandoned.
