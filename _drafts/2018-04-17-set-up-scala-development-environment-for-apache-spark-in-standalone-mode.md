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

With the Apache Spark installed through the steps described in [last post](http://leifengblog.net/blog/install-apache-spark-in-standalone-mode-on-windows/), this post will instroduce the steps to set up a Scala development environment for Spark and build a WrodCount application through Maven and SBT. 

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

### Install SBT

SBT is a build tool for Scala, Java, and others. You can download the latest `.msi` for Windows from [https://www.scala-sbt.org/download.html](https://www.scala-sbt.org/download.html) After download, doouble-click to install. 


### Install Maven

You can download Maven from [http://maven.apache.org/download.cgi](http://maven.apache.org/download.cgi). CLick and downlaod the latest version  `apache-maven-x.x.x-bin.zip`. At the time of this writing, the latest version is `apache-maven-3.5.3-bin.zip`. Extract the downloaded zip file to C drive, such as `C:\apache-maven-3.5.3`.

**Set MAVEN_HOME Variables**

Set environmental variables:
- Varaiable: MAVEN_HOME
- Value: C:\apache-maven-3.5.3  (or your installation path)
Add `%MAVEN_HOME%\bin` to `PATH` variable.

You can check the installation with following command in `cmd`:
```
mvn -version
```

**Set Maven in Eclipse**

Open the installed Scal IDE, navigate to **Window**|**Preference** in Eclipse and open **Maven** in the left pane of the **Preference** window. Click on the **Installations** and then click on the **Add** button to select the lcoation of the Maven directory (e.g.`C:\apache-maven-3.5.3`). Then select the added installation  to launch Maven, as shwon in following screenshot:

![MavenSettings01.PNG]({{site.baseurl}}/img/post/MavenSettings01.PNG)

Then go click the **User Settings** browser to corresponding *settings.xml* files for Global and User settings:

![MavenSettings02.PNG]({{site.baseurl}}/img/post/MavenSettings02.PNG)

If you are behind proxy, you might need to set the proxies through **open file** link:

![MavenSettings03.PNG]({{site.baseurl}}/img/post/MavenSettings03.PNG)

## Build WordCount Application

In this section, we are going build WordCount applications through Scala IDE, sbt, and MAVEN. The three applications are shared through [Github repository](https://github.com/stonefl/SparkExamples).

The source code for `WordCount` scala object is shown as below:
```scala
package com.learningspark.example.WordCount
import org.apache.spark._
import org.apache.spark.SparkContext._
import org.apache.log4j._

object WordCount {
  /** Our main function where the action happens */
  def main(args: Array[String]) {
   
    // Set the log level to only print errors
    Logger.getLogger("org").setLevel(Level.ERROR)
    
     // Create a SparkContext using every core of the local machine
    val sc = new SparkContext(new SparkConf().setAppName("Spark Word Count").setMaster("local"))  
    
    // Read each line of my book into an RDD
    val input = sc.textFile("../book.txt")
    
    // Split into words separated by a space character
    val words = input.flatMap(x => x.split(" "))
    
    // Count up the occurrences of each word
    val wordCounts = words.countByValue()
    
    // Print the results.
    wordCounts.foreach(println)
  }
 
}
```


