---
layout: post
title:      "CLI Revelations"
date:       2019-03-08 23:31:40 -0500
permalink:  cli_revelations
---

I got through a lot of the labs leading up to our first project by finding solutions and then working backwards to understand what I was seeing and how I might have made it my own. Because of this, I was worried that creating a CLI gem from scratch would prove far more difficult than any of the prior lessons. The example provided for our project, World's Best Restaurants, was very close to what I wanted to create and did help later on, but scraping the information I wanted wasn't something I could see elsewhere and did indeed prove to be the biggest challenge for me.

I spent a lot of time trying to scrape the year of release for each film from the main list page:
https://letterboxd.com/visdave34/list/the-official-letterboxd-top-250-movies-updated/

I never did figure out how to do so, and from what I can see by opening the full page's HTML in Repl.it and searching for "1972", The Godfather's date, it doesn't seem to actually exist there aside from a short description object that lists the first five films. I was stubborn about trying to find it, though, because I could see it shown here when inspecting:

![](https://i.imgur.com/9xyZgD9.png)

In retrospect, there was no need to push myself to figure it out, since I knew I would eventually need to iterate over each film's own page in order to get the other data I wanted. It provided a good lesson in self-restraint and taught me that it can be more helpful to move to another segment when I'm having difficulty, rather than push myself for too long on something giving me trouble.

While the data I wanted was much easier to scrape from the film's own pages, I ran into a similar issue when trying to scrape the average user rating for each film. It appeared to be easily accessible, and so I caught tunnel vision again trying to figure out how to call on it.

![](https://i.imgur.com/GZaCp9M.png)

Calling this section or the deeper "span.average-rating" section, however, failed to return anything other than empty arrays. Viewing the full HTML for the page showed me that the rating I wanted, "4.55", was *somewhere* in there, and I was having trouble extracting it. I finally found myself going yet another url level deeper to with the following roundabout code:

```
histogram_url = film_page.css("div.js-csi")[1].attribute("data-src").value
histogram = Nokogiri::HTML(open("https://letterboxd.com#{histogram_url}"))
@rating ||= histogram.css("span.average-rating").css("a").attribute("title").value.match(/\d\D\d{2}/).to_s
```

It wasn't until this was working that I realized I could go back and use the section's index number to get a much cleaner, one line solution:

```
@rating ||= film_page.css("meta")[17].attribute("content").value[0..3]
```

Being able to see the smaller collection under `film_page.css("div.js-csi")` helped me realize that I had not been thinking of the HTML in terms of index numbers and instead only in terms of searchable class names. It was a lesson in continuing with your code and creating something that works first in order to find patterns that can help you shorten your ideas later.

Thankfully, writing the CLI portion of the code was much easier once I had my Film objects all created. I'm glad I put my focus on the scraping portion of the gem first, as it gave me time to think of how I could rewrite my scraping lines while doing the rest. It also helped me find some other minor things in testing that I wanted to change, such as films with multiple directors displaying incorrectly.

There's still a few lines I would love to find ways to write better, but I'm happy with what I was able to learn so far and how it ultimately came out.
