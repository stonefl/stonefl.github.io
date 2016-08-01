---
layout: post
author: stonefl
comments: true
date: 'Wed Jul 01 2015 16:07:33 GMT-0500 (Central Daylight Time)'
link: >-
  https://leifengtechblog.wordpress.com/2015/07/01/benefits-of-constraint-programming/
slug: benefits-of-constraint-programming
title: Benefits of Constraint Programming
wordpress_id: 95
categories:
  - Operations Research
tags:
  - Constraint Programming
  - Optimization
published: true
---

Constraints Programming (CP) is a relatively new, but evolving rapidly, paradigm in Operation Research. It was derived from Computer Science - Logic Programming, Graph Theory, and Artificial Intelligence. Like a Mathematical Programming (MP), such as Linear Programming, Integer Programming, or Nonlinear Program, CP works with the same concepts of decision variables, constraints, and/or objective function. Because of its flexible modeling language and powerful search strategy, CP is a powerful and easy-to-use optimization technology to solve highly combinatorial optimization problems, such as scheduling problems, timetabling problems, sequencing problems, and allocation or rostering problems. These problems might be difficult to solve for traditional MP, due to: 1) constraints that are nonlinear in nature; 2) a con-convex solution space that contains many locally optimal solutions; 3) multiple disjunctions, which result in poor information returned by a linear relaxation of the problem. This post tries to summarize some major benefits of CP in contrast with MP models in modeling and solving standpoints.
<!--more-->


## Intuitive Modeling Language


Comparing to MP, CP allows more flexible modeling language, which is be more intuitive and closer to natural language. Virtually any expression over the variables is allowed.


### Wide Types of Decision Variables




The decision variables types include the classical binary, integer, and continuous. Unlike in integer programming, where the range of a variable is specified and maintained as an interval, in constraint programming, the variables are maintained explicitly as a set of elements that is called _**domain**_.  In addition, CP can model special "structured" variable types. One example of this special variable types is the set variables that take a set of elements as value. Another example is activities or interval variables that are suitable to model the scheduling and sequence problem.




### Nearly All Kinds of Constraints Expressions


With the explicit element representation, CP allows wider types of constraints to be defined by arbitrary expressions through algebraic or logical operators. Specially, logical constraints, such as AND, OR, NOT and IF-THEN, and 'global constraints', such as FORALL, EXISTS, SUM, ALLDIFFERENT can be easily formulated in CP. Here are some example expressions:

Arithmetic Expressions: x²·(y²-z) ≥ 25 + x²· max(x, y, z)

Extensional Constraints('Table' Constraints): (x, y, z) in MyTupleSet

Variables as Subscripts ('Element' Constraints): y = cost(x), where y and x are variables, 'cost' is an array of parameters.

Reasoning with meta-constraints: ∑i (xi > Ti) ≤ 5

Logical rations in which (meta-) constraints can be mixed: if ((x < y) OR (y < z)) then c = min(x, y)

Global Constraints: Alldifferent(x1, x2, ..., xn)

In general, CP contraints can be non-linear, non-differentiable, and discontinuous.


### With or Without Objective Function


Depending on with or without an objective function, constraint programming models can be categorized into two types: constraint optimization problem (COP) with an objective function and constraint satisfaction problem (CSP) without an objective function. COP aims to find an optimal solution, while CSP can provide a feasible solution or proves that no solution exists.


## Powerful Search Strategy




The solving process underlying CP involves a systematic search over a search space. Initially, the search space contains all combinations of the values in the domains of all decision variables. To avoid exploring the entire search space, CP first removes inconsistent values from the domains of the variables involved in each constraint. Then a search strategy (depth first, width first or multi-start) is applied to guide the search for a solution within the reduced search space. The search process can be viewed as traversing a tree, where the root is the starting point, a leaf node is a combination of values in the reduced search space and each branch represents a move (branching) within the search. Each leaf node is evaluated to determine if it will produce a feasible solution. A solution is a set of value assignments to the decision variables such that each variable is assigned to exactly one value from its domain.




[![download](https://leifengtechblog.files.wordpress.com/2015/07/download.png?w=300)](https://leifengtechblog.files.wordpress.com/2015/07/download.png)





## Combination With Other Solution Framework


Constraint programming can also be used as a fast generator of feasible solutions. This can be extremely useful in combination with other models and engines, for instance to implement [column generation](http://www.or.rwth-aachen.de/research/publications/primer.pdf) for a complex optimization model.


## References





	
  1. [AIMMS Language Reference - Constraint Programming ](http://www.aimms.com/aimms/download/manuals/aimms3lr_constraintprogramming.pdf)

	
  2. _Willem-Jan van Hoeve. Introduction to Constraint Programming_ and _Operations Research Techniques in Constraint Programming_. [ACP Summer School on Constraint Programming](http://www.andrew.cmu.edu/user/vanhoeve/summerschool/), 2012.
