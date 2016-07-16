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

[Markdown](https://en.wikipedia.org/wiki/Markdown) is a way to write web content. Formatting text in Markdown doesn't do anything fancy like changing font size, color, or type in CSS, instead it only defines different formatting elements through putting a few symbols, such as asterisks(`*`) and backticks(`` ` ``), around plaintext to display the plaintext as bold, headers, lists, code blocks, etc. Technically speaking, Markdown is simplier than HTML and CSS to format your web content. This is one of the reasons why I moved my blog from Wordpress.com to Github Pages. In this post I listed out some frequently used formatting elements syntax in Markdown. It have been used it as a quick reference for my daily writing.
<!--more-->



## Table of Content



## 1. Block Elements

### 1.1 Paragraphs and Breaks

Paragraphs consist of one or more consecutive lines of text that are separated by one or more blank lines. If a line contains only spaces, it is a blank line. Blocks of text separated by one or more blank lines will be parsed as paragraphs. If you want to create a line break, simply end a line with two or more spaces, then hit Return/Enter.

### 1.2 Headers

Headers work as titles and subtiles for sections. To create a header, simply prefix your header text with the number of hash marks (`#`) to specify heading depth. For example: # Header 1, ## Header 2 and ### Header 3 will be progressively smaller headers. You can end your headers with any number of hashes.

### 1.3 Blockquotes

A blockquote is a sentence or paragraph from another source that's been specially formatted to draw attention to the reader. To create a block quote, all you have to do is preface a line or a paragraph with the "greater than" caret ('>'). For example:
<pre>
> "In a few moments he was barefoot, his stockings folded in his pockets and his
  canvas shoes dangling by their knotted laces over his shoulders and, picking a
  pointed salt-eaten stick out of the jetsam among the rocks, he clambered down
  the slope of the breakwater."
</pre>
would generate a blockquote as:
> "In a few moments he was barefoot, his stockings folded in his pockets and his
  canvas shoes dangling by their knotted laces over his shoulders and, picking a
  pointed salt-eaten stick out of the jetsam among the rocks, he clambered down
  the slope of the breakwater."

**Note:** if you decide to hard-wrap text, you need to prefix each line of your quote with a > character.

### 1.4 Lists

Markdown supports both ordered and unordered lists. To create an ordered list, simply prefix each line with a number (any number will do — this is why the editor only uses one number.) To create an unordered list, you can prefix each line with '*', '+' or '-'.

List items can contain multiple paragraphs, however each paragraph must be indented by at least 4 spaces or a tab.

In Markdown, you can list items using numbers, a +, a -, or a '*'. However, if the first item in a list or sublist is numbered, Markdown will interpret the entire list as ordered and will automatically number the items linearly, no matter what character you use to denote any given separate item.




  

### References

[Mastering Markdown](https://guides.github.com/features/mastering-markdown/)
[Markdown Tutorial](http://markdowntutorial.com/)

  



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
