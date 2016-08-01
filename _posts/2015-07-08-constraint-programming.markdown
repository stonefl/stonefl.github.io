---
layout: post
author: stonefl
comments: true
date: 'Wed Jul 08 2015 10:30:48 GMT-0500 (Central Daylight Time)'
link: 'https://leifengtechblog.wordpress.com/2015/07/08/constraint-programming/'
slug: constraint-programming
title: Solve Einstein's Logic Puzzle through Constraint Programming in AIMMS
wordpress_id: 2
categories:
  - Operations Research
  - Constraint Programming
tags:
  - Constraint Programming
  - Logic Puzzle
published: false
---



A brain teaser has been posed by Albert Einstein, who claimed that 98% of population in the world could not figure it out . I have tried with hands on it, unfortunately, I didn't find a solution within half an hour. Thus, I built a Constraint Programming (CP) model in AIMMS to solve it. If you are interested, try your hand on it first. If you belong to that lucky 2%, please let me know how long it took you. If not, you can check out the CP model below for a solution.






Here is the puzzle, copied from [Begent](http://www.begent.org/einstein.htm) for completeness:







**FACTS:**








	
  1. There are 5 houses in 5 different colors.

	
  2. In each house lives a person with a different nationality.

	
  3. These 5 owners drink a certain beverage, smoke a certain brand of cigarette and keep a certain pet.

	
  4. No owners have the same pet, brand of cigarette, or drink.







**CLUES:**








	
  1. The Brit lives in a red house.

	
  2. The Swede keeps a dog.

	
  3. The Dane drinks tea.

	
  4. The green house is on the left of the white house.

	
  5. The green house owner drinks coffee.

	
  6. The person who smokes Pall Mall keeps birds.

	
  7. The owner of the yellow house smokes Dunhill.

	
  8. The man living in the house right in the center drinks milk

	
  9. The Norwegian lives in the first house.

	
  10. The man who smokes Blends lives next to the one who keeps cats.

	
  11. The man who keeps horses lives next to the man who smokes Dunhill.

	
  12. The owner who smokes Camel drinks beer.

	
  13. The German smokes Marlborough.

	
  14. The Norwegian lives next to the blue house.

	
  15. The man who smokes Blends has a neighbor who drinks water.









The question is, **who keeps the fish**?









### Mathematical Modeling






From mathematical perspective, this puzzle can be formulated as a combinatorial optimization problem. It can be converted to a problem that orders 5 sets (Nationality, House, Pet, Drink, and Smoke), each of which has 5 elements. The ordering has to satisfy above facts and clues. Elements in these sets with the same order correspond  to a statement of 'which _person_ lives in which_ house_, keeps which_ pet_, drinks which _beverage_ and smokes which _cigarette_'. Then the question 'who keeps the fish' can be answered.

I formulated and solved this puzzle as a Constraint Satisfaction Problem(CSP) in AIMMS. CSP which is a Constraint Programming (CP) model without objective function. The post [Benefits of Constraint Programming](https://leifengtechblog.wordpress.com/2015/07/01/benefits-of-constraint-programming/) gives an introduction of CP. Readers are referred to [AIMMS-The Language Reference](http://www.aimms.com/aimms/download/manuals/aimms3lr_constraintprogramming.pdf) for more details on CP and associated modeling language in AIMMS. The built AIMMS CP model and interface are provided next.









### Implementation in AIMMS







A CSP model called 'Einstein_Puzzle' was defined as below.




#### Model Definition




MAIN MODEL Main_Einstein_Puzzle




  DECLARATION SECTION 







    SET:




       identifier   :  Houses




       index        :  h




       definition   :  data {'red','white','green','yellow','blue'} ;







    SET:




       identifier   :  Nationalities




       index        :  n




       definition   :  data {'Brit','Swede','Dane','Norwegian','German'} ;







    SET:




       identifier   :  Drinks




       index        :  d




       definition   :  data {'tea','coffee','milk','beer','water'} ;







    SET:




       identifier   :  Pets




       index        :  p




       definition   :  data {'dog','birds','cats','horses','fish'} ;







    SET:




       identifier   :  Smokes




       index        :  s




       definition   :  data {'Pall Mall','Dunhill','Blends','Camel','Marlborough'} ;







    ELEMENT VARIABLE:




       identifier   :  eV




       range        :  Nationalities ;







    VARIABLE:




       identifier   :  House




       index domain :  h




       range        :  {1..5} ;







    VARIABLE:




       identifier   :  National




       index domain :  n




       range        :  {1..5} ;







    VARIABLE:




       identifier   :  Drink




       index domain :  d




       range        :  {1..5} ;







    VARIABLE:




       identifier   :  Pet




       index domain :  p




       range        :  {1..5} ;







    VARIABLE:




       identifier   :  Smoke




       index domain :  s




       range        :  {1..5} ;







    CONSTRAINT:




       identifier   :  Fact01




       definition   :  CP::AllDifferent(h,House(h)) ;







    CONSTRAINT:




       identifier   :  Fact02




       definition   :  CP::AllDifferent(n, National(n)) ;







    CONSTRAINT:




       identifier   :  Fact03




       definition   :  CP::AllDifferent(d,Drink(d)) ;







    CONSTRAINT:




       identifier   :  Fact04




       definition   :  CP::AllDifferent(p,Pet(p)) ;







    CONSTRAINT:




       identifier   :  Fact05




       definition   :  CP::AllDifferent(s,Smoke(s)) ;







    CONSTRAINT:




       identifier   :  Clue01




       definition   :  National('Brit') = House('red')




       comment      :  "The Brit lives in a red house" ;







    CONSTRAINT:




       identifier   :  Clue02




       definition   :  National('Swede') =Pet('dog')




       comment      :  "The Swede keeps a dog" ;







    CONSTRAINT:




       identifier   :  Clue03




       definition   :  National('Dane') =Drink('tea')




       comment      :  "The Dane drinks tea" ;







    CONSTRAINT:




       identifier   :  Clue04




       definition   :  House('green') = House('white')-1




       comment      :  "The green house is on the left of the white house." ;







    CONSTRAINT:




       identifier   :  Clue05




       definition   :  House('green') = Drink('coffee')




       comment      :  "The green house owner drinks coffee." ;







    CONSTRAINT:




       identifier   :  Clue06




       definition   :  Smoke('Pall Mall') = Pet('birds')




       comment      :  "The person who smokes Pall Mall keeps birds." ;







    CONSTRAINT:




       identifier   :  Clue07




       definition   :  House('yellow') = Smoke('Dunhill')




       comment      :  "The owner of the yellow house smokes Dunhill." ;







    CONSTRAINT:




       identifier   :  Clue08




       definition   :  Drink('milk') = 3




       comment      :  "The man living in the house right in the center drinks milk" ;







    CONSTRAINT:




       identifier   :  Clue09




       definition   :  National('Norwegian') =1




       comment      :  "The Norwegian lives in the first house." ;







    CONSTRAINT:




       identifier   :  Clue10




       definition   :  abs(Smoke('Blends')-Pet('cats'))=1




       comment      :  "The man who smokes Blend lives next to the one who keeps cats" ;







    CONSTRAINT:




       identifier   :  Clue11




       definition   :  abs(Pet('horses')-Smoke('Dunhill'))=1




       comment      :  "The man who keeps horses lives next to the man who smokes Dunhill" ;







    CONSTRAINT:




       identifier   :  Clue12




       definition   :  Smoke('Camel') = Drink('beer')




       comment      :  "The owner who smokes Camel drinks beer" ;







    CONSTRAINT:




       identifier   :  Clue13




       definition   :  National('German') = Smoke('Marlborough')




       comment      :  "The German smokes Marlborough." ;







    CONSTRAINT:




       identifier   :  Clue14




       definition   :  abs(National('Norwegian')-House('blue'))=1




       comment      :  "The Norwegian lives next to the blue house" ;







    CONSTRAINT:




       identifier   :  Clue15




       definition   :  abs(Smoke('Blends')-Drink('water'))=1




       comment      :  "The man who smokes Blend has a neighbour who drinks water." ;







    CONSTRAINT:




       identifier   :  Question




       definition   :  National(ev)=Pet('fish')




       comment      :  "Who owns the pet fish? Result stored in element variable eV" ;







    MATHEMATICAL PROGRAM:




       identifier   :  EinsteinPuzzle




       direction    :  minimize




       constraints  :  AllConstraints




       variables    :  AllVariables




       type         :  CSP ;







  ENDSECTION  ;







  PROCEDURE




    identifier :  MainInitialization







  ENDPROCEDURE  ;







  PROCEDURE




    identifier :  MainExecution




    body       :  




      solve EinsteinPuzzle;




      







  ENDPROCEDURE  ;







  PROCEDURE




    identifier :  MainTermination




    body       :  




      return DataManagementExit();







  ENDPROCEDURE  ;







ENDMODEL Main_Einstein_Puzzle ;







#### Model Interface




Below shows the model interface and obtained solution. From the solution, one can conclude that the German keeps fish. In addition, one can also conclude other facts, such as 'the Norwegian lives in yellow house, keeps cats, drinks water, and smokes Dunhill'.







[![](https://leifengtechblog.files.wordpress.com/2015/07/f91b3-capture.png)](https://leifengtechblog.files.wordpress.com/2015/07/f91b3-capture.png)










#### Question:




Is this solution unique? Can you find out other feasible solution?




Please feel free go leave your answers, comments or suggestions. Any feedback is welcome.
