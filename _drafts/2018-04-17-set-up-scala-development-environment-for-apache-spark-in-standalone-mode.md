---
layout: post
published: false
title: 'Set Up Scala Development Environment for Apache Spark in Standalone Mode '
subtitle: Learning Apache Spark Tutorial
date: '2017-08-28'
categories:
  - Tutorial
tags:
  - Apache Spark
---

With the Apache Spark installed through the steps described in [last post](http://leifengblog.net/blog/install-apache-spark-in-standalone-mode-on-windows/), this post will instroduce the steps to set up a Scala development environment for  Spark and build a word count application through Scala IDE, Maven, and SBT. 

Althrough Spark can be linked in applications through either Java, Scala, or Python, this post will focus on Scala, which has couple of reasons: 1) Spark itself is written in Scala; 2) Scala's functional programming model is a good fit for distributed processing, which has less code and boilerplate stuff than Java; 3) Scala compiles to Java bytecode, which gives faster performance than Python.  
<!--more-->

## Table of Content
{:.no_toc}

* TOC
{:toc}
