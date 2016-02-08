---
layout: post
title: "An Injection of Ruby"
date: 2016-02-08 18:11:03 -0500
comments: true
categories: "Flatiron School"
---



Before last week I was convinced that at a fundamental level everything could be built of some combination of an if, else and while loop. I ignored higher level enumerators at all cost. As soon as I saw Ruby's inject method I instinctively tried to avoid it. It seemed confusing and unnecessary. Maybe there were some “advanced” coders who used it but I’m sure I could get around ever needing it.

At some point during last week's lab I was prodding into using it and very quickly the learning curve disappeared and its benefits was obvious.<br>

Enumerable#inject is a powerful shortcut, it’s a good tool to avoid writing lines of unnecessary code.<br>

For the record the basics of inject can be done with some clunky code:<br>

```
counter = 5
sum = 0
while counter <= 10
  sum += 5
  counter += 1
end
return sum
```

So what is inject? Inject is an iterating device lets you pass it a variable that can then be acted upon by all the items that are iterated through. Think of it like a global variable that stays throughout the laps of iteration. Inject then returns the variable.<br>

A basic example would work like this:
```
[2,3,4].inject() do | accumulator, item|
  accumulator += item
end
#=> 9
```

Every item in the range is passed into the inject method. The block is executed one for each element that the inject is called up, in this case the range array with numbers 2,3 and 4. The block will be executed upon 3 times. The first time the variable ‘item’ will be ‘2’, the second ‘3’ and the third ‘4’. In each execution the ‘item’ will be added to the ‘accumulator’ variable. Inject is an easy way to sum up all the items in the array! Think of what else it can do!<br>

Inject can also be passed a variable so that your ‘accumulator’ doesn’t need to to start at 0. Take a look at this example. The ‘accumulator’ variable is going to start at 20. This information is set directly to the right of the inject method.<br>


```
[2,3,4].inject(20) do | accumulator, item|
  accumulator += item
end
#=> 29
```