---
layout: post
author: stonefl
comments: true
date: 'Mon Jul 13 2015 23:12:38 GMT-0500 (Central Daylight Time)'
link: >-
  https://leifengtechblog.wordpress.com/2015/07/13/a-generic-comparator-class-for-java-collections-sort/
slug: a-generic-comparator-class-for-java-collections-sort
title: A Generic Comparator Class for Java Collections.sort()
wordpress_id: 22
post_format:
  - Aside
tags:
  - Java
  - Generics
published: false
categories:
  - Programming Language
---

### Sort A List of Objects




As a Java programmer, I often need to sort a list of objects. If the object is a primitive type, such as `String, Integer, Long, Float, Double, or Date,` it is easy to use `[Collections.sort()](https://docs.oracle.com/javase/tutorial/collections/interfaces/order.html)`. However, to sort a list of user defined objects, which do not implement the `Comparable `interface, for example, to sort a list of **Person** objects, as defined below, by id in ascending order, one has to provide a [Comparator](https://docs.oracle.com/javase/8/docs/api/java/util/Comparator.html) - an object that encapsulates an ordering.




[code language="java" collapse="false" title="Person.java"]
public class Person {
    //fields
    private int id;
    private String name;
    private Payment pay;
    //constructor
    public Person(String name, int id,
                   int startSal, int startBon){
        this.name = name;
        this.id = id;
        this.pay = new Payment(startSal, startBon);
    }
    //method get name
    public String getName(){
        return name;
    }
    //method get id
    public int getId(){
        return id;
    }
    //method get start salary
    public int getStartSalary(){
        return pay.startSalary;
    }
    //method get start bonus
    public int getStartBonus(){
       return pay.startBonus;
    }
    //inner payment class
    private class Payment{
       int startSalary;
       int startBonus;
       public Payment(int sal, int bon){
          this.startSalary = sal;
          this.startBonus = bon;
       }
    }
}
[/code]

One possible Comparator class with above aim might be:

[code language="java" collapse="true" title="SortPersonById.java"]
import java.util.Comparator;

public class SortPersonById implements Comparator&lt;Person&gt;{
	@Override
	public int compare(Person p1, Person p2) {
		if(p1.getId() &gt; p2.getId()){
			return 1;
		} else if (p1.getId() &lt; p2.getId()){
			return -1;
		} else {
			return 0;
		}
	}
}
[/code]

Then one can use

[code language="java" gutter="false"] Collections.sort(personList, new SortPersonById()); [/code]

to sort the list ` personList ` by id in ascending order.


### Generic Comparator




What if the user wants to sort the `personList` by `name` instead of the `id`? or in descending order instead of ascending? It is tedious to write one class for each of these situation. Is there any generic way to it? A [GenericComparator](https://github.com/stonefl/GenericComparator/blob/master/src/GenericComparator.java) class proposed in this post can be used to sort any object by any declared field in any specified order. The reflection technology is used for accessing fields in the class. This generic class can be used to sort lists of primitive as well as user defined objects.


There are two constructors, as shown below. **Constructor 1 **defines default ascending order and the sort field names. Please note, the varargs format of sort field names are used for different level of fields. For example, in the `Person` Class above, the first level of payment field is "pay" and the second level of field names in the "pay" field are "startSalary" and "startBonus". **Constructor 2** works in the same way, excepts the user defined sorting order.

[code language="java" collapse="false" title="Constructor 1"]
public GenericComparator(String... sortFieldNames) {
    this.bAscendingOrder = true;
    this.sfieldNames = sortFieldNames;
}
[/code]


[code language="java" collapse="false" title="Constructor 2"]
public GenericComparator(final boolean sortAscending, 
                          String... sortFieldNames) {
    this.bAscendingOrder = sortAscending;
    this.sfieldNames = sortFieldNames;
}
[/code]



### How to Use


An example is posted here to illustrate how to use the GenericComparator class.




[code language="java" collapse="false" title="TestGenericComparator.java"]
import java.util.ArrayList;
import java.util.Collections;
import java.util.List;

public class TestGenericComparator {

 public static void main(String[] args) {
    // Build a list of persons with different names and ids
    List&lt;Person&gt; personList = new ArrayList&lt;Person&gt;();
    personList.add(new Person("Angela", 102, 50000, 5000));
    personList.add(new Person("Mike",101, 65000, 5500));
    personList.add(new Person("Lisa", 104, 75000,4500));
    personList.add(new Person("Bob", 103, 58000, 4300));
    //print initial person list
    printPersonList(personList);

    //sort personList by name field
    Collections.sort(personList, new GenericComparator("name"));
    printPersonList(personList);
    //sort personList by id field in ascending order
    Collections.sort(personList, new GenericComparator(true,"id"));
    printPersonList(personList);
    //sort personList by id field in descending order
    Collections.sort(personList, new GenericComparator(false,"id"));
    printPersonList(personList);
    //sort personList by pay field's start salary
    Collections.sort(personList, new GenericComparator("pay","startSalary"));
    printPersonList(personList);

    //test primitive list
    List&lt;Integer&gt; iList = new ArrayList&lt;Integer&gt;();
    iList.add(12);
    iList.add(15);
    iList.add(13);
    iList.add(20);
    System.out.println(iList);

    //sort iList in descending order
   Collections.sort(iList, new GenericComparator(false));
    System.out.println(iList);
 }

 /**
 * Print person list.
 * @param personList
 */
 private static void printPersonList(List&lt;Person&gt; personList) {
    for(Person p: personList){
        System.out.println(p.getName() + "\t" + p.getId() + "\t"
                       + p.getStartSalary() + "\t" +p.getStartBonus());
    }
    System.out.println("-------------");
 }

}

[/code]




Execution results:
`
Angela 102 50000 5000
Mike 101 65000 5500
Lisa 104 75000 4500
Bob 103 58000 4300
-------------
Angela 102 50000 5000
Bob 103 58000 4300
Lisa 104 75000 4500
Mike 101 65000 5500
-------------
Mike 101 65000 5500
Angela 102 50000 5000
Bob 103 58000 4300
Lisa 104 75000 4500
-------------
Lisa 104 75000 4500
Bob 103 58000 4300
Angela 102 50000 5000
Mike 101 65000 5500
-------------
Angela 102 50000 5000
Bob 103 58000 4300
Mike 101 65000 5500
Lisa 104 75000 4500
-------------
[12, 15, 13, 20]
[20, 15, 13, 12]
`
Detailed source code and implement examples are available through [GitHub](https://github.com/stonefl/GenericComparator.git).


### Reference


1. Making a Generic Comparator Class: [http://stackoverflow.com/questions/15189949/making-a-generic-comparator-class](http://stackoverflow.com/questions/15189949/making-a-generic-comparator-class)

2. Generic Comparator in Java: [http://myjeeva.com/generic-comparator-in-java.html](http://myjeeva.com/generic-comparator-in-java.html)
