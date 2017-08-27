---
layout: post
published: false
title: Install Apache Spark in a standalone mode on Windows
subtitle: Learning Apache Spark Tutorial
tags:
  - Apache Spark
categories:
  - Tutorial
author: stonefl
comments: true
---
**Apache Spark** is a cluster comuting framework for large-scale data processing, which aims to run programs in parallel across many nodes in a cluster of computers or virtual machines. It comibnes a stack of libraries including **SQL and DataFrames**, **MLlib** for machine learnign, **GraphX**, and **Spark Streaming**. Spark can run in four modes:
- The standalone local mode where all Spark processes run within the same JVM process
- The standalone cluster mode which uses Spark's own built-in, job-scheduling framework
- [Apache Mesos](https://mesos.apache.org/)
- [Hadoop YARN](https://hadoop.apache.org/docs/current/hadoop-yarn/hadoop-yarn-site/YARN.html)

As Spark's local mode is fully compatible with cluster modes, thus the local mode is very useful for prototyping, developing, debugging, and testing. Programs written and tested locally can be run on a cluster with just a few additional steps. In addition, the standalone mode can also be used in real-world scenarios to perform parallel computating across multiple cores on a single computer. In this post, I will go through steps of setting up Spark in standalone mode. 
<!--more-->






