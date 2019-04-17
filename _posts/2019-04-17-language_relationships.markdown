---
layout: post
title:      "Language Relationships"
date:       2019-04-17 22:43:10 +0000
permalink:  language_relationships
---

One of the things I first struggled with when moving from the Object Oriented Ruby section to SQL was understanding the way that the two languages interacted with one another within the same program. It was initially jarring to read and write tables with completely new terms. And unlike pry, which also launched within the terminal, the sqlite3 gem introduced a new set of commands and inserted data into the program that had to be called in order to view it, rather than accepting familiar Ruby commands and returning its values.

This became much easier to understand once I reached the section on SQL querying, since it reads in a similar order to the way one would write queries in English. For example, here you can transale the query as "Select the title and year of each book within the first series and order them by year," making it easier to follow exactly what you are selecting and where you are getting that data.

![](https://i.imgur.com/t8l7Rsr.png)

Ruby enumerables that iterate over collections (each, collect, detect, etc.) work in a more abstract way, since you first call them on a collection and then manipulate a new variable that each element of that collection passes through. Learning SQL queries made it easier to think about how these two ways of working with data were related. While they initially appeared to be constructed in entirely different ways, thinking about them by their base elements revealed how similar they were.

![](https://i.imgur.com/NQLLdKb.png)

Inserting a group of data into a table, like above, is similar to mass initializing a group of objects. The table title is similar to the class of an object, and, rather than object ids, each has a primary key id by default when created. Much like the default initialize class method in OOR, SQL inserting accepts an argument of variables that you then pass data through in order to store. The above example shows a set of data being inserted into a table and how the data corresponds to the argument variables.

Viewing these separate elements as what they are and what they do within each language allowed me to draw the parallels I needed to link the two together. Realizing this, I learned a way of approaching new material that will help me going forward to understand concepts more quickly even when there is a difference in the language being used.
