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

With the Apache Spark installed through the steps described in [last post](http://leifengblog.net/blog/install-apache-spark-in-standalone-mode-on-windows/), this post will instroduce the steps to set up a Scala development environment for Spark and build a WrodCount application through Scala IDE, Maven, and SBT. 

Althrough Spark can be linked in applications through either Java, Scala, or Python, this post will focus on Scala, which has couple of reasons: 1) Spark itself is written in Scala; 2) Scala's functional programming model is a good fit for distributed processing, which has less code and boilerplate stuff than Java; 3) Scala compiles to Java bytecode, which gives faster performance than Python.  
<!--more-->

## Table of Content
{:.no_toc}

* TOC
{:toc}

## Installations and Settings

### Install Scala IDE for Eclipse

You can download the lastest version from [http://scala-ide.org/download/sdk.html](http://scala-ide.org/download/sdk.html). At the time of this writing, the latest version is 4.7.0 which is based on the Eclipse 4.7(Oxygen) with Scala 2.12. After download, simply extract it into a folder, such as `C:\eclipse`.

### Install Scala (optional)

Because the Scala IDE includes Scala versions, it is optional to install Scala programming language locally. But if you want to try Scala in an interactive way, you can download the latest Scala binary for windows from the [download page of scala](http://www.scala-lang.org/download) and keep track where you isntalled (e.g.`C:\Program Files (x86)\scala`).

**Set SCALA_HOME Variables**

Set environmental variables:
- Varaiable: SCALA_HOME
- Value: C:\Program Files (x86)\scala  (or your installation path)
Add `%SCALA_HOME%\bin` to `PATH` variable.

You can check the installation with following command in `cmd`:
```
scala -version
```
### Install Maven

You can download Maven from [http://maven.apache.org/download.cgi](http://maven.apache.org/download.cgi). CLick and downlaod the latest version  `apache-maven-x.x.x-bin.zip`. At the time of this writing, the latest version is `apache-maven-3.3.9-bin.zip`. Extract the downloaded zip file to C drive, such as `C:\apache-maven-3.3.9`.

**Set MAVEN_HOME Variables**
Set environmental variables:
- Varaiable: MAVEN_HOME
- Value: C:\apache-maven-3.3.9  (or your installation path)
Add `%MAVEN_HOME%\bin` to `PATH` variable.

You can check the installation with following command in `cmd`:
```
mvn -version
```

**Set Maven in Eclipse**

Open the installed Scal IDE, go to `Window` --> `Preferences` --> `Maven` --> `Installations`, shown as below:



### Install SBT



