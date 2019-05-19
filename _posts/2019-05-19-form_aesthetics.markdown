---
layout: post
title:      "Form Aesthetics"
date:       2019-05-19 20:46:12 +0000
permalink:  form_aesthetics
---


When I first began my Sinatra project, I was able to fulfill all of the requirements with basic text input forms for my User and Deck classes. However, I was bothered by the lack of realism in keeping the decks that way. I personally know that the game has a limited number of formats in which each deck could be played and a limited number of colors that cards can be, so I wanted to limit users from being able to set those fields as whatever they wanted. I also disliked the way that decklists would paste and display as a single paragraph rather than a list of line items. In the end I was able to research and implement unique form input types for each of these elements in order to create a more logical and aesthetically pleasing form for users:

![](https://i.imgur.com/2dlcWju.pnghttp://)

The first input type I knew I wanted to implement was the checkbox input for colors, since a previous lesson showed us how to iterate over a Pet class and give them to Owners upon creation. I first tried to follow that example and create a class variable set to an array of the colors I wanted. However, after a few attempts to run that code through the erbs I discovered a [resource](https://www.w3schools.com/html/html_form_input_types.asp) with all of the html form input types and much easier method:

```
<p><label for="colors">Color(s): </label>
  <input type="checkbox" name="colors[]" value="Black">Black
  <input type="checkbox" name="colors[]" value="Blue">Blue
  <input type="checkbox" name="colors[]" value="Green">Green
  <input type="checkbox" name="colors[]" value="Red">Red
  <input type="checkbox" name="colors[]" value="White">White
  <input type="checkbox" name="colors[]" value="Colorless">Colorless
```

The above code instead inputs any number of the checked options into the colors param for a given deck, and allowed me to return those choices easily by performing `colors: params[:colors].join(", ")` when creating each deck. This fulfilled my desire for users to be able to pick any color combination they wanted when creating a deck, so long as they existed within the game as well.

I continued to browse w3schools after this, searching for a way to build a drop down menu for my deck format choices. While I could have utilized checkboxes again, decks are typically not played within multiple formats even when the rules allow for it, so I wanted users to have to choose a main format for each deck instead. Eventually, I discovered an [article](https://www.w3schools.com/html/html_form_elements.asp) that taught me about the select tag.

```
<select name="format" id="format">
    <option value="Standard">Standard</option>
    <option value="Modern">Modern</option>
    <option value="Legacy">Legacy</option>
    <option value="Vintage">Vintage</option>
    <option value="Commander">Commander</option>
  </select>
	```
	
This input type also has a range of options that would have allowed me to customize how the drop down list displays for users (number of options displayed, number that can be selected, etc.). However, since I only wanted users to choose one format for each deck, the default construction worked for me. I am, however, glad to know that it is customizable in and of itself should I ever find myself wanting to use that in the future.

The last thing I wanted to change was to add a larger input field for decklists. I was lucky enough to find the textarea input type explained right below select, and was able to quickly implement it into my project and set the exact column and row numbers I wanted to display the size text area I liked. It allowed me to paste in decklists with the line breaks I wanted and kept that when moving to the edit pages. However, when displaying deck pages, the field was again having the line breaks ignored and combining it into a paragraph instead.

I consider using Regex to split the text and then iterate over it to display it back, but wasn't having any luck getting the display I wanted and was confused as to why it displayed correctly in the saved edit textarea field. After some time I was eventually able to discover the white-space CSS property. I was able to set a div class around my textarea in the display erb (`<div class="decklist"><br><%= @deck.decklist %></div>`) and then set the white-space to the preset value I wanted in my stylesheet:

```
div.decklist {
    white-space: pre-wrap;
  }
```

What began as a minor annoyance to me ended with me learning a number of useful html commands and drastically changing my project. That itself served as a great lesson for not settling on code that works if I have an idea for something greater. Researching my options helped me come out with something that still worked, but left me more satisfied with that work.
