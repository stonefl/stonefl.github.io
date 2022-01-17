---
layout: post
published: true
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


DS and OR are both powerful analytics disciplines and work in different paradigms. The nature of the analytical problem should determine the choice of the discipline/technique.


## DS and OR are Used at Different Stages of Analysis

The Gartner Analytics Ascendency Mode identifies four main types of analytics: descriptive, diagnostic, predictive, and prescriptive. Each addresses the following questions:
1. Descriptive Analytics: What happened?
2. Diagnostic Analytics: Why did it happen?
3. Predictive Analytics: What will happen in the future?
4. Prescriptive Analytics: What should I do to improve the outcome?

![data science]({{site.baseurl}}/img/post/ds_03.png)

Picture comes from ([Gartner.com](https://www.gartner.com/en))

While people separate the above four analytics into categories/types, I would argue that they are linked together and build upon each other. As one moves from simple analytics to more complex ones, the degree of difficulty increases and, at the same time, generates more value.

Recall that statistics, data mining, and machine learning are the three primary techniques in the DS domain. **Statistical analysis** is known as descriptive analytics providing the information/hindsight of what happened; **Data Mining** works as diagnostic analytics that provides insights on why it happened; **Machine Learning** is the predictive analytics that answers the foresight on what will happen. Thus the first three stages of analytics correspond to the three primary techniques from DS domain. Lastly, OR goes with prescriptive analytics that seeks optimal solutions to better decisions.

The following table summarizes the differences between DS and OR from multiple dimensions.

|  	| Data Science 	| Operations Research 	|  	|  	|
|:---:	|---	|---	|---	|---	|
| Capability 	| Descriptive, Diagnostic, and Predictive 	| Prescriptive 	|  	|  	|
| Business Value 	| Knowledge and actional insights 	| Optimal or near-optimal actions/strategies/decisions 	|  	|  	|
| Quantitative Tools 	| Statistics, Data Mining and Machine Learning Models, Artificial Intelligence 	| Mathematical Modeling, Optimization Algorithms, Heuristics 	|  	|  	|
| Popular Algorithms 	| Linear Regression, Logistic Regression, Support Vector Machine, Decision Tree, Neural Network  	| Linear Programming, Integer Programming, Dynamic Programming, Graph/Network Algorithms 	|  	|  	|
| Software/Platforms 	| SAS, Sci-kit Learning, Spark, TensorFlow, Python, 	| CPLEX, Gurobi, OR-tools, Java, C++, Python 	|  	|  	|
| Paradigm 	| Data-Centric 	| Problem-Centric 	|  	|  	|
| Project Steps 	| Opportunity statement<br>Data acquisition<br>Data exploration and opportunity reframing if needed<br>Model creation and Training<br>Iterative model evaluation<br>Modeling deployment 	| Identification of the problem<br>Mathematical modeling/formulation of business objective and constraints<br>Data acquisition if needed<br>Iterative modeling and refinement<br>Modeling deployment 	|  	|  	|
| Business Application Examples 	| Shipment volume forecasting<br>Delivery time estimating<br>Predictive fleet maintenance and fuel economy 	| Optimize stop sequence to minimize travel distance and time for pickup and delivery<br>Optimize network design and volume routing to minimize transportation cost  	|  	|  	|
| Data and Computation Requirements 	| Data needs are extensive to learn underlying patterns<br>Data storage and processing power needs could be very high 	| Data needs are lower than data science<br>The processing power required to solve mathematical models could be very high 	|  	|  	|


## DS and OR Overlap and Work Together


Although DS and OR work in different paradigms and cover different stages of analysis, they are closely relevant and overlapped. 

### Share Common Knowledge and Skills

Both of them require mathetics, statistics, and computer science knowledge. DS has considerable overlap with OR in statistical analysis, which uses advanced statistical inferences, models, and theories to find meaning in large data sets. In the big data era, practitioners in DS and OR need to know how to use computers, clusters, and cloud computing to quickly analyze large amounts of data from different sources in various formats and types for useful insights.

### ML Rely on Optimization

Machine Learning (ML) models of DS rely on optimization algorithms. Notice that training any ML models always involves solving an optimization problem. For supervised ML models, for example, the process of training Linear or Logistic Regression models is finding a line or a curve to minimize error or loss. As one example for unsupervised ML models, the K-means clustering model is to partition data points to minimize the distances to centroids. Even the reinforcement learning models, where agents take actions to maximize cumulative rewards.

Based on the above two facts, it is relatively easy for an OR professional to transfer to a Data Scientist through limited ML and AI training. However, picking up required skills in OR requires rather significant amounts of effort, usually deserves a full-time Ph.D.

## DS and OR Work Together

DS and OR enable companies to transform data into information, information into insights, and insights into better decisions in today's competitive environments.

![data science]({{site.baseurl}}/img/post/ds_04.png)

The graph above illustrates the journey from data to business value. Data is the fuel that powers data science's vehicle that generates actionable insights. The data foundation contains the strategies of data ingestion, data storage, and management. Data science analyzes data to predict the future and provide actionable insights. Optimization engines are created for the best decisions for business values maximization under different situations or constraints.

Whether your domains are in DS or OR, your job is solving problems, answering questions, increasing revenue, reducing cost, improving efficiency, and adding business values through delivering effective solutions. I'm still enjoying these.
