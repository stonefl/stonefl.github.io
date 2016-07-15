---
layout: post
title: A Quick Reference of Markdown
subtitle: A learning note of Markdown
published: true
categories:
  - Programming
tags: Markdown
date: '2016-07-13'
---

[Markdown](https://en.wikipedia.org/wiki/Markdown) is a way to write web content. Formatting text in Markdown doesn't do anything fancy, like changing font size, color, or type in CSS, instead it only define different formatting elements through putting a few symbols, such as asterisks(`*`) and backticks(`` ` ``), around plaintext to display the plaintext as bold, headers, lists, code blocks, etc. Technically speaking, Markdown is simplier than HTML and CSS to format your web content. This is one of the reasons why I moved my blog from Wordpress.com to Github Pages. 
<!--more-->

This post lists out some frequently used formatting elements syntax in Markdown. It have been used as a quick reference for my daily writing. Some of the examples I used here come from [Markdown Tutorial](http://markdowntutorial.com/) and I highly encourage you to take 5 minutes to learn how to write in markdown. 

# Table of Content



# 1. Block Elements

## 1.1 Paragraph and Line Breaks

Paragraphs consist of one or more consecutive lines of text and they are separated by one or more blank lines. If a line contains only spaces, it is a blank line. Blocks of text separated by one or more blank lines will be parsed as paragraphs. If you want to create a line break, simply end a line with two or more spaces, then hit Return/Enter.

## 1.2 Headers

Header work as titles and subtiles for sections. To create a header, simply prefix your header text with the number of hash marks (`#`) to specify heading depth. For example: # Header 1, ## Header 2 and ### Header 3 will be progressively smaller headers. You can end your headers with any number of hashes.

## 1.3 Blockquotes

A blockquote is a sentence or paragraph from another source that's been specially formatted to draw attention to the reader. To create a block quote, all you have to do is preface a line with the "greater than" caret ('>'). For example:

<tt>
> "In a few moments he was barefoot, his stockings folded in his pockets and his
  canvas shoes dangling by their knotted laces over his shoulders and, picking a
  pointed salt-eaten stick out of the jetsam among the rocks, he clambered down
  the slope of the breakwater."
</tt>

would generate a blockquote:

> "In a few moments he was barefoot, his stockings folded in his pockets and his
  canvas shoes dangling by their knotted laces over his shoulders and, picking a
  pointed salt-eaten stick out of the jetsam among the rocks, he clambered down
  the slope of the breakwater."

** Note: ** if you decide to hard-wrap text, if need to prefix each line of your quote with a > character.





  


  



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
