---
layout: post
title: A Quick Reference of Markdown
subtitle: A learning note of Markdown
category: dev
tag: markdown
published: true
categories:
  - Programming
tags: Markdown
date: '2016-07-13'
---

Markdown is a way to write web content. Formatting text in Markdown doesn't do anything fancy, like changing font size, color, or type in CSS, instead it only define different formatting elements through putting a few symbols, such as asterisks(`*`) and backticks(`` ` ``), around plaintext to display the plaintext as bold, headers, lists, code blocks, etc. Technically speaking, Markdown is simplier than HTML and CSS to format your web content. This is one of the reasons why I moved my blog from Wordpress.com to Github Pages. 
<!--more-->

This post lists out some frequently used formatting elements in Markdown. It is used as a quick reference for my daily writing. Some of the examples I used here come [Markdown Tutorial](http://markdowntutorial.com/), and I highly encourage you to take 5 minutes to learn how to write in markdown. 




I strongly encourage you to [take 5 minutes to learn how to write in markdown]([http://markdowntutorial.com/](http://markdowntutorial.com/)) - it'll teach you how to transform regular text into bold/italics/headings/tables/etc.

**Here is some bold text**


## Here is a secondary heading

Here's a useless table:
 
| Number | Next number | Previous number |
| :------ |:--- | :--- |
| Five | Six | Four |
| Ten | Eleven | Nine |
| Seven | Eight | Six |
| Two | Three | One |
 

How about a yummy crepe?

![Crepe](http://lafenicegelato.com/wp-content/uploads/2014/09/crepes-with-chocolate.jpg)

Here's a code chunk:

~~~
x <- 5 + 10
print(x)
~~~

And here is some code with syntax highlighting

```javascript
var foo = function(x) {
  return(x + 5);
}
foo(3)
```
