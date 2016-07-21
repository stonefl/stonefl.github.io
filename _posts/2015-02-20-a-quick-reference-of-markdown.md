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

* [1. Block Elements](#1.-Block-Elements)
  + [1.1 Paragraphs and Breaks](#1.1-Paragraphs-and-Breaks)
* [2. Span Elements](#span-elements)


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

Markdown supports both ordered and unordered lists. To create an ordered list, simply prefix each line with a number and a dot `.`. To create an unordered list, you can prefix each line with one of the characters `*`, `+` or `-`. One list item can contain multiple paragraphs, however each paragraph must be indented by at least 4 spaces or a tab. For example:
<pre>
1. Fruit:
    * Pears
    * Peaches
    * Apples 
        + Granny Smith 
        + Gala
    * Oranges
    * Bananas
2. Dairy:
    - Milk
        + Whole
        + Skim
</pre>
will be interpreted as:

1. Fruit:
    * Pears
    * Peaches
    * Apples 
        + Granny Smith 
        + Gala
    * Oranges
    * Bananas
2. Dairy:
    - Milk
        + Whole
        + Skim
        
### 1.5 Code Blocks

Code can either in the middle of a paragraph ([Inline Code](#inline-code)), or as a block. To include a complete code-block, you can use triple backquotes. Optionally, you can put the name of the language that you are quoting after the starting triple backquotes, like this:
<pre>
```python
def plusOne(n):
    return n + 1
```
</pre>
That will format the code-block (sometimes called "fenced code") with syntax coloring. The above code block would be rendered like:

```python
def plusOne(n):
    return n + 1
```

### 1.6 Section Blocks

Sections can be separated by horizontal rules, which are created by placing three or more hyphens('-'), underscores(' _ ') or asterisks(' * ') on a line by themselves, for example:
<pre>
---
___

***
</pre>
will create three horizontal rules:

---

___


***

## 2. Span Elements

### 2.1 Style and Emphsis

In most of browsers, text surrounded with asterisks (` * `) or underscores (` _ `) are displayed as italics, while text surrounded by double asterisks (` ** `) or double underscores (` __ `) are rendered as bold. 

**Note:** There is no space between the starting asterisks and the text.

### 2.2 Inline Code

You can use a single backtick (`` ` ``) to start and stop code in the middle of a paragraph. Here's an example:
<pre>
The word `function` will appear in a code-like form.
</pre>
The word `function` will appear in a code-like form.

If you want to include a literal backtick in your code, you can suround the whole text block in double backticks like this:
<pre>
Look at this literal `` backtick` ``
</pre>
Look at this literal `` backtick` ``

### 2.3 Links


<http://en.wikipedia.org>

Markdown has two types of links: inline and reference. For both types of links, the text you want to display to the user is placed in square brackets. For example, if you want your link to display the text “GitHub”, you write [GitHub].

To create an inline link, create a set of parentheses immediately after the brackets and write your URL within the parentheses. (e.g., [GitHub](http://github.com/)). Relative paths are allowed in inline links.

To create a reference link, use two sets of square brackets. [my internal link][internal-ref] will link to the internal reference internal-ref.

If you want to create a link that displays the actual URL, Markdown allows you to quickly wrap the URL in '<' and '>' to do so. For example, the link http://github.com/ is easily produced by writing <http://github.com/>.




  

### References

1. [Mastering Markdown](https://guides.github.com/features/mastering-markdown/)
2. [Markdown Tutorial](http://markdowntutorial.com/)
