---
layout: post
published: false
title: Data Science vs. Operations Research in Advanced Analytics
thumbnail: /img/post/dashboard.jpg
categories:
  - Operations Research
  - Data Science
date: '2022-01-16'
---

Both Data Science (DS) and Operations Research (OR) are two disciplines that provide advanced analytics capabilities. They are highly relevant and overlapped, but they work in two different paradigms. In this post, I'm trying to explain the relationship between DS and OR, the differences, and how they could work together in advanced analytics based on my experience in DS and OR.
<!--more-->

![dashboard]({{site.baseurl}}/img/post/dashboard.jpg)
Picture comes from ([https://unsplash.com/@goumbik](https://unsplash.com/photos/mcSDtbWXUZU))

Let's get started with the description of DS and OR.


## What are DS and OR?

**Data Science (DS)** has become a popular buzzy word since 2011. Here is the definition from [Wikipedia](https://en.wikipedia.org/wiki/Data_science):
> DS  is an interdisciplinary field that uses scientific methods, processes, algorithms, and systems to extract knowledge and insights from noisy, structured, and unstructured data and apply knowledge and actionable insights from data across a broad range of application domains. Data science is related to data mining, machine learning, and big data.

From the above definition, we can see that DS is a mixture study of maths/statistics, computer science, and an understanding of business problems. DS uses **statistics**, **data mining**,  and **machine learning** to extract knowledge and insights from data to inform, direct, and predict business. As its name indicates, DS starts from the data, usually big data.

![data science]({{site.baseurl}}/img/post/ds_01.png)


**Operations Research (OR)**, compared to DS, has a long history. OR originated in military planning efforts during World War II, and today it is applied widely in business, industry, and society. It is a discipline that applies analytical methods to find optimal or near-optimal solutions to decision-making problems. The analytical methods include various problem-solving techniques, such as statistical analysis, simulation, optimization, queueing theory, stochastic process, etc. OR is a study of making better decisions and usually starts with a real-world problem to be solved.

The following picture illustrates the typical steps of an OR problem-solving process. The practical nature of OR forces the process to start from understanding real-world business problems. OR practitioners will translate the business problem into one or more generic OR problems or their variants, such as Traveling Salesman Problem (TSP), Vehicle Routing Problem (VRP), Facility Location/Routing Problem, etc. The translated generic OR problems will be modeled in mathematical ways through Linear, Integer, or Mixed-Integer Programmings and get solved through various searching, heuristic, and dynamic programming algorithms.  

![data science]({{site.baseurl}}/img/post/ds_02.png)

Picture comes from ([Big Picture of Operations Research](https://towardsdatascience.com/the-big-picture-of-operations-research-8652d5153aad))

















