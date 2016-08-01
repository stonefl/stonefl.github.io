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

After installed IBM ILOG CPLEX Optimization Studio 12.6, I tried the instructions described in the [IBM Knowledge Center](http://www-01.ibm.com/support/knowledgecenter/SSSA5P_12.6.0/ilog.odms.cplex.help/CPLEX/GettingStarted/topics/set_up/Eclipse.html) to set up Java APIs for CPLEX and CP in Eclipse, but they do not work correctly. Here is what I did to build a java project with CPLEX  and CP Java APIs in Eclipse.

These steps have been done in Eclipse on Window 7, not sure if it works for other Java IDEs or other OSs. It also assumes that the IBM ILOG CPLEX Optimization Studio has already been installed.
<!--more-->

* Create a new Java project in Eclipse, through **File**->**New**…>**Java Project**

* Import a java file from the example folder to the ‘**src**’ folder of the built project.

	* For CPLEX, in my case, they are located at: C:\Program Files\IBM\ILOG\CPLEX_Studio126\ cplex\examples\src\java
    * For CP, the examples are located at: C:\Program Files\IBM\ILOG\CPLEX_Studio126\ cpoptimizer\examples\src\java

* Include the JAR library to the project, through right click on project then **Properties**** **> **Java Build Path**** **> **Libraries, **then** Add External JARs.**

* Browse to the location **‘oplall.jar’**, which is located at **C:\Program Files\IBM\ILOG\CPLEX_Studio126\opl\lib** in my case. Select this jar file and add it to the library.

* Make sure the CPLEX STUDIO BINARIES is included in the PATH environmental variables. In my case the path is **C:\Program Files\IBM\ILOG\CPLEX_Studio126\ opl\bin\x64_win64. **

In my case, I defined a system variable with name of **CPLEX_STUDIO_BINARIES126** and value of
**C:\Program Files\IBM\ILOG\CPLEX_Studio126\ opl\bin\x64_win64;
 C:\Program Files\IBM\ILOG\CPLEX_Studio126\ opl\oplide\;
 C:\Program Files\IBM\ILOG\CPLEX_Studio126\ cplex\bin\x64_win64;
 C:\Program Files\IBM\ILOG\CPLEX_Studio126\ cpoptimizer\bin\x64_win64**. 
 Then add **%CPLEX_STUDIO_BINARIES126%** to the PATH.

* Now you can run your project through **Run As > Java Application**


The last 2 steps are different to the description from above link. In addition, I found that the ‘**oplall.jar**’ works for both CP and CPLEX.
