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
---

[Markdown](http://markdowntutorial.com/) is a way to write content for the web. You can write regular Markdown in your post and Jekyll will automatically covert it to a nice webpage. Formatting text in Markdown does not do anything fancy like change font size, color, or type in CSS. All you have control over are displaying plaintext bold, creating headers, and organizing lists and blocks through a few symbols, such as asterisks(` * `) and backticks(`` ` ``). Therefore, Markdown is simplier and faster than HTML and CSS to format web content.
<!--more-->

This 

You can write regular [markdown](http://markdowntutorial.com/) here and Jekyll will automatically convert it to a nice webpage.  I strongly encourage you to [take 5 minutes to learn how to write in markdown](http://markdowntutorial.com/) - it'll teach you how to transform regular text into bold/italics/headings/tables/etc.

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
