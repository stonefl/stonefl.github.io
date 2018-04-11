---
layout: post
published: false
title: Install Apache Spark in a Standalone Mode on Windows
subtitle: Learning Apache Spark Tutorial
tags:
  - Apache Spark
categories:
  - Tutorial
author: stonefl
comments: true
---
**Apache Spark** is a cluster comuting framework for large-scale data processing, which aims to run programs in parallel across many nodes in a cluster of computers or virtual machines. It comibnes a stack of libraries including **SQL and DataFrames**, **MLlib**, **GraphX**, and **Spark Streaming**. Spark can run in four modes:
- The standalone local mode where all Spark processes run within the same JVM process.
- The standalone cluster mode which uses Spark's own built-in, job-scheduling framework.
- [Apache Mesos](https://mesos.apache.org/), where driver runs on the master work nodes run on separat machines.
- [Hadoop YARN](https://hadoop.apache.org/docs/current/hadoop-yarn/hadoop-yarn-site/YARN.html), where the underlying storage is HDFS. Driver runs inside an application master process which is managed by YARN on the cluster and work nodes run on different data nodes.

As Spark's local mode is fully compatible with cluster modes, thus the local mode is very useful for prototyping, developing, debugging, and testing. Programs written and tested locally can be run on a cluster with just a few additional steps. In addition, the standalone mode can also be used in real-world scenarios to perform parallel computating across multiple cores on a single computer. In this post, I will walk through the stpes of setting up Spark in a standalone mode on Windows 10. 
<!--more-->

## Table of Content
{:.no_toc}

* TOC
{:toc}


### Step 1. Install Java (7 or above)

Spark process runs in JVM. Java should be installed on the machines on which you are about to run Spark job. 
Download Java 8 JDK from the Oracle [download page](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html) and keep track of where you installed the JDK (e.g. `C:\Program Files\Java\jdk1.8.0_161`). You will need it later. 

**Set JAVA_HOME Variables**
Set environmental variables:
- Varaiable: JAVA_HOME
- Value: C:\Program Files\Java\jdk1.8.0_161  (or your installation path)
Add `%JAVA_HOME%\bin` to `PATH` variable.

After the installation, you can run following command to check if Java is installed correctly:
```
java -version
```
If everything is fine, you will get similar response below:
```
java version "1.8.0_161"
Java(TM) SE Runtime Environment (build 1.8.0_161-b12)
Java HotSpot(TM) 64-Bit Server VM (build 25.161-b12, mixed mode)
```

### Install Scala (2.10.x or above)

Download the Scala(2.10.5) binary for windows from the [download page of scala](http://www.scala-lang.org/download/2.10.5.html) and keep track where you isntalled (e.g.`C:\Program Files (x86)\scala`).

**Set SCALA_HOME Variables**
Set environmental variables:
- Varaiable: SCALA_HOME
- Value: C:\Program Files (x86)\scala  (or your installation path)
Add `%SCALA_HOME%\bin` to `PATH` variable.

You can check the installation with (you might need to restart your `cmd`):
```
scala -version
```

### Install Hadoop


### Install Spark



