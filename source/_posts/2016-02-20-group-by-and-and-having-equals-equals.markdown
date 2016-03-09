---
layout: post
title: "Group By &amp;&amp; Having == ?"
date: 2016-02-20 21:41:16 -0500
comments: true
categories: "Flatiron School"
---

Let's talk about the GROUP BY and HAVING statements and how to best use them in SQL.

But first ... ROTHKO!

<img src="https://www.etc.cmu.edu/projects/atl/images/rothko/rothko3.jpg">

Why Rothko? His work highlights the importance of carefully choosing the items that group together. By "grouping" specific colors  the piece as a whole is stronger than the individual color. Grouping or picking the right items that go together can heighten or take away from a group. 1 + 1 = 3 or 1 + 1 = -2.
<br ><br >
<strong>Further Proof on the importance of correctly grouping items</strong>

Same with food, eating a meal that has flavors that complement each other can bring the plate to the next level (salty and sweet is a killer... shout out to salted crack caramel ice cream).

<img src="https://sprungonfood.files.wordpress.com/2014/08/image_36.jpeg">

<strong>1. Group By</strong>

What’s up with GROUP BY? Is it as straightforward as it sounds or is there some dark layer hiding underneath that will haunt your SQL statement and return you 'american cheese' when you were expecting 'Gouda'. SQL acts like it's as straight forward as vanilla but there's got to be some chunky monkey hiding beneath the surface. (No more food jokes, I promise.)

<strong>Group By - Basics:</strong>

Lots of times we have more than one record for a certain attribute. For example, there could be 25 players on the Yankees  in a league with hundreds of players. What if I just want to know how many home runs the Yankees' hit?

OR what if need to know the total sick days for 5 members of the custodial staff in a company of 100 employees?

OR what if I'm trying to see the average age of the current members of Parliament Funkadelic and my database has info on everyone who has ever played in the group?

GROUP BY is the key to finding out this kind of critical information in a SQL database.

GROUP BY gathers all of the rows together that contain data in the specified column and will allow aggregate functions to happen to one or more columns.

Let's say you are in charge of a zoo. Let's call it the <i>Flatiron Zoo for Discarded Animals</i>. To keep better records you put together a nice SQL database that looks like this:

<img src="http://www.joshzizmor.com/fi/sql.png">



Let’s say I’d like to see how many Mammals I have at my small zoo. I’d want to have a row just for animal types. That’s where GROUP BY can come in handy. I can SUM the items in my select and only show one row of Animal Type.

I'd execute this SELECT to see how many of each animal type there is.
```
SELECT type, SUM(QTY) FROM animals
GROUP BY type

```
<img src="http://www.joshzizmor.com/fi/sql2.png">

<strong>Be Aware, be very aware:</strong>

There must be some common missteps that people make, right?

Let's say you run this SQL statement:

```
SELECT * FROM animals
GROUP BY type

```

You would get a highly dubious table that looks something like this:<br>
<img src="http://www.joshzizmor.com/fi/sql3.png">

It probably wouldn't be much help since it's basically just given us one row for each animal type.



<br>
<strong>2. HAVING</strong><br>

So what's the deal with using HAVING? I know it replaces WHERE sometimes but what's the rule... when should I be using it?

<ol><li><strong>RULE #1:</strong> WHERE does not work with aggregates. For example:
```
SELECT animal_type, sum(Qty) from Animals_in_zoo
GROUP BY animal_type WHERE sum(qty) > 10
```
This does not work. You need a HAVING instead of WHERE if there's an aggregate involved. It should look like this:
```
SELECT animal_type, sum(Qty) from Animals_in_zoo
GROUP BY animal_type HAVING sum(qty) > 10</li>
```

<li><strong>RULE #2: </strong>One of the SELECT items has an AS after it.

SELECT animal_type, animal AS animalize from Animals_in_zoo
GROUP BY animal_type HAVING animalize = 'Duck'</li></ol>

Now More ROTHKO

<img src="https://upload.wikimedia.org/wikipedia/en/5/5f/No_61_Mark_Rothko.jpg" >
