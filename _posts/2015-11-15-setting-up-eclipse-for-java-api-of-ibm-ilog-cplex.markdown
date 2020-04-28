---
layout: post
author: stonefl
comments: true
date: 'Sat Nov 14 2015 22:03:26 GMT-0600 (Central Standard Time)'
link: >-
  https://leifengtechblog.wordpress.com/2015/11/14/setting-up-eclipse-for-java-api-of-ibm-ilog-cplex/
slug: setting-up-eclipse-for-java-api-of-ibm-ilog-cplex
title: Setting up Eclipse for Java API of IBM ILOG CPLEX
wordpress_id: 148
tags:
  - Java
  - ILOG CPLEX
published: true
categories:
  - Operations Research
---

**Upated on April 28, 2020 with testing on Windows 10.**

After installed IBM ILOG CPLEX Optimization Studio 12.6, I tried the instructions described in the [IBM Knowledge Center](http://www-01.ibm.com/support/knowledgecenter/SSSA5P_12.6.0/ilog.odms.cplex.help/CPLEX/GettingStarted/topics/set_up/Eclipse.html) to set up Java APIs for CPLEX and CP in Eclipse, but the instructions did not work correctly. Here is what I did to build a java project with CPLEX  and CP Java APIs in Eclipse.

These steps have been done in Eclipse on Windows 7 and 10, not sure if it works for other Java IDEs or other OSs. It also assumes that the IBM ILOG CPLEX Optimization Studio has already been installed.

<!--more-->

* Step 1: Create a new Java project in Eclipse, through **File**->**New**…>**Java Project**

* Step 2: Import a java file from the example folder to the ‘**src**’ folder of the built project.

	* For CPLEX, in my case, they are located at: C:\Program Files\IBM\ILOG\CPLEX_Studio126\ cplex\examples\src\java
    * For CP, the examples are located at: C:\Program Files\IBM\ILOG\CPLEX_Studio126\ cpoptimizer\examples\src\java

* Step 3: Include the JAR library to the project, through right click on project then **Properties**** **> **Java Build Path**** **> **Libraries**, then **Add External JARs**.

* Step 4: Browse to the location **oplall.jar**, which is located at **C:\Program Files\IBM\ILOG\CPLEX_Studio126\opl\lib** in my case. Select this jar file and add it to the library.

* Step 5: Make sure the CPLEX STUDIO BINARIES is included in the PATH environmental variables. You can follow the processes below on Windows:
     - Open **Enrironment Variables** settings, create a new user variable. Set name to  `CPLEX_STUDIO_BINARIES126` and value as
     ```
     C:\Program Files\IBM\ILOG\CPLEX_Studio126\opl\bin\x64_win64;    
     C:\Program Files\IBM\ILOG\CPLEX_Studio126\opl\oplide\; 
     C:\Program Files\IBM\ILOG\CPLEX_Studio126\cplex\bin\x64_win64;
     C:\Program Files\IBM\ILOG\CPLEX_Studio126\cpoptimizer\bin\x64_win64**
     ```
![cplex_studio_variable.JPG]({{site.baseurl}}/img/cplex_studio_variable.JPG)

     - Double click on the `PATH` in the user variables. Create a new item with the value as `%CPLEX_STUDIO_BINARIES126%`


Now you can run your project through **Run As > Java Application**


The Steps 4 and 5 are different to the description from above link. In addition, I found that the ‘**oplall.jar**’ works for both CP and CPLEX.
