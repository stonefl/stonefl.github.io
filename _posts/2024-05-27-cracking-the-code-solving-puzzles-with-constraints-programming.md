---
layout: post
published: false
title: 'Cracking the Code: Solving Puzzles with Constraints Programming'
date: '2024-05-27'
categories:
  - constraintprogramming
  - optimization
  - AI
thumbnail: /img/post/cp_image.webp
---

Have you ever got stumped by a logic puzzle? Sukodu got you scratching your head? Einstein’s puzzle made you crazy with the clues and facts? These puzzles might seem like mental gymnastics, but there’s a secret weapon can be used to crack the code: Constraint Programming (CP).
<!--more-->

## What Makes CP Special?
CP has emerged as a powerful paradigm within Operation Research, offering a unique approach using logic and constraints to find elegant solutions to complex optimization problems. Drawing inspiration from Computer Science fields like Logic Programming, Graph Theory, and Artificial Intelligence, CP becomes a powerful tool for optimization problems in various fields.

Both CP and traditional Mathematical Programming (MP) deal with decision variables, constraints, and/or objective functions. But CP stands out with a few key features:

- **Intuitive Modeling Language**: CP utilizes a flexible and natural language-like approach to model problems. This allows for the inclusion of virtually any expression over the variables, surpassing the limitations of MP in terms of:
- **Wide Variety of Decision Variables**: CP supports classical binary, integer, and continuous variables, but also introduces “structured” variable types like sets, activities, and intervals, ideal for scheduling and sequencing problems.
- **Diverse Constraint Expressions**: CP embraces a wider range of constraints, including arbitrary algebraic and logical expressions, “global constraints,” and even reasoning with meta-constraints.
- **Powerful Search Strategy**: CP employs a systematic search process to navigate the problem space. Starting with all possible value combinations, it progressively prunes inconsistent values based on the defined constraints. This search strategy, guided by various algorithms like depth-first or width-first search, efficiently explores the reduced search space to find feasible solutions.
- **Flexibility in Problem Formulation**: CP models can be categorized as Constraint Optimization Problems (COP) with an objective function or Constraint Satisfaction Problems (CSP) without one. This flexibility allows for finding optimal solutions or simply confirming the existence of feasible solutions.
- **Combination with Other Frameworks**: CP’s ability to generate feasible solutions rapidly makes it valuable in conjunction with other optimization models and engines, such as implementing column generation in complex problems.

## Einstein’s Puzzle

Einstein’s puzzle is a brain teaser was claimed created by Albert Einstein, who claimed that 98% of population in the world could not figure it out.

![einstein's puzzle]({{site.baseurl}}/img/post/einstein_puzzle.webp)

**Here is the Einstein's Puzzle:**

**FACTS:**
1. There are 5 houses in 5 different colors.
2. In each house lives a person with a different nationality.
3. These 5 owners drink a certain beverage, smoke a certain brand of cigarette and keep a certain pet. No owners have the same pet, brand of cigarette, or drink.

**CLUES:**
1. The Brit lives in a red house.
2. The Swede keeps a dog.
3. The Dane drinks tea.
4. The green house is on the left of the white house.
5. The green house owner drinks coffee.
6. The person who smokes Pall Mall keeps birds.
7. The owner of the yellow house smokes Dunhill.
8. The man living in the house right in the center drinks milk.
9. The Norwegian lives in the first house.
10. The man who smokes Blends lives next to the one who keeps cats.
11. The man who keeps horses lives next to the man who smokes Dunhill.
12. The owner who smokes Camel drinks beer.
13. The German smokes Marlborough.
14. The Norwegian lives next to the blue house.
15. The man who smokes Blends has a neighbor who drinks water.

The question is, **who keeps the fish**?


From mathematical perspective, the Einstein’s Puzzle can be formulated as a combinatorial optimization problem. It can be converted to a problem that orders 5 sets (Nationality, House, Pet, Drink, and Smoke), each of which has 5 elements. The ordering has to satisfy above facts and clues. Elements in these sets with the same order correspond to a statement of ‘which person lives in which house, keeps which pet, drinks which beverage and smokes which cigarette‘. Then the question ‘who keeps the fish’ can be answered.

Before looking at the solution notebook below, you are encouraged to try to solve it by hand to feel why it is supposedly too tough for 98% of population.

If you got stuck, no worries! You are welcome to check out the notebook below to see how CP solves it with ease. Here is the notebook I created for the solution using google’s OR-tools.



<script src="https://gist.github.com/stonefl/e58711cb9b39b5be2675726d2e6916c6.js"></script>















