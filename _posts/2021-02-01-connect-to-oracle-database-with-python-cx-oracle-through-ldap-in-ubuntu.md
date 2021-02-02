---
layout: post
published: true
title: Connect to Oracle Database with Python cx_Oracle through LDAP in Ubuntu
thumbnail: /img/post/mylaptop.jpg
date: '2021-01-31'
categories:
  - Programming
tags:
  - Python
  - Oracle
---
Connecting to Oracle Database with Python cx_Oracle through LDAP is not trivial. It needs to install cx_Oracle module and Oracle Instant Client libraries, as well as LDAP settings in the Oracle Client. This post describes the processes I followed to set up the connection to an Oracle Database on-premises with Python on a Ubuntu 18.04 LTS Virtual Machine on Microsoft Azure. 

<!--more-->
## Connection Architecture
The following picture shows the connection architcture, where the users run a Python program that calls the cx_Oracle module. The cx_Oracle module loads Oracle Client libraries that provide the necessary network connectivity to access an Oracle Database instance. Thus, to connect to a remote Oracle Database, we need to install both cx_Oracle moduel and Oracle Client libraries. 

![bye-2020]({{site.baseurl}}/img/post/cx_Oracle_arch.png)
                  
Picture comes from ([cx_Oracle Architecture](https://cx-oracle.readthedocs.io/en/latest/_images/cx_Oracle_arch.png))

## Install cx_Oracle
* Check your Python versions through the following commands to make sure you have Python 3 installed.
```
python --version
python3 --version
```
In my case, on my VM I have both Python 2.7 and Python 3.6 installed. All the following steps are for Python 3.

* Before installation of cx_Oracle, you might need to install pip for Python 3 on Ubuntu VM through the following commands:
```
sudo apt update && sudo apt install python3-pip
```
* With pip3 installed, you run the following command to install cx_Oracle
```
pip3 install cx_Oracle
```

## Install Oracle Client
There are multiple ways to install the Oracle Cient, the following describes the steps to install an Oracle Instant Client through the zip files:

* Download the latest version "Basic" or "Basic Light" zip file from the Instant Client download page[64-bit](https://www.oracle.com/database/technologies/instant-client/linux-x86-64-downloads.html) or [32-bit](https://www.oracle.com/database/technologies/instant-client/linux-x86-32-downloads.html)

* Unzip the package into a single directory that is accessible to your application. For example:
```
sudo mkdir -p /opt/oracle
sudo unzip instantclient-basic-linux.x64-21.1.0.0.0.zip -d /opt/oracle/
```
* Install `libaio` package with sudo or as the root user. This package is also called `libaio1` in some distributions. For example, in my case I need to run:
```
sudo apt install libaio1
```
* Add the following line in the `$HOME/.bashrc` file and run `source .bashrc` to refresh the settings.
```
export LD_LIBRARY_PATH=/opt/oracle/instantclient_21_1
```
* Create subdirectory `network/admin` within the directory `opt/oracle/instantclient_21_1/`, if it is not created yet.
* In the `network/admin` subdirectory, create two files of `sqlnet.ora` with the following content:
```
# sqlnet.ora
# Place this file in the network/admin subdirectory or your 
# $ORACLE_HOME location.
NAMES.DIRECTORY_PATH = (LDAP)
```

and `ldap.ora` with the content below:
```
# ldap.ora
# Place this file in the network/admin subdirectory or your 
# $ORACLE_HOME location.
DIRECTORY_SERVERS = ([ldapservername:ldapport])
DEFAULT_ADMIN_CONTEXT = "[DomainContext]"
DIRECTORY_SERVER_TYPE = OID
```
Note: you need to update the content in the brackets with your own information.

The picture above shows an example of Custom JDBC connection to an Oracle Databasev in SQL Developer. The conncetion string in the Custom JDBC URL box usually has the format below:
```
jdbc:oracle:thin:@ldap://[ldapservername:ldapport]/[DBservicename],[DomainContext]
```
![custom jdbc url]({{site.baseurl}}/img/post/sql_developer01.PNG)


## Connect to Oracle Database in Python

With the above installation and configurations, the following Python scripts can be used to connect to the Oracle Database. The scripts is pretty self-explained, but you need to note the **[DBservicename]** in the scripts: if your OID is created with only `cn=OracleContext`, then you need to append a dot (.) at the end of service name. For my case, my service name is ABC_DEFG and the OID is created only context of `cn=OracleContext`, I need to specify the server as `ABC_DEFG.`.

```
'''
A Python scripts that:
    1) get the username and password for the oracle database;
    2) read sql query from a file
    3) run the query and print out column metadata
'''
import cx_Oracle
import getpass # library to input password

try: 
    # input username and password
    username = input("Please enter your FDW username: ")
    password = getpass.getpass("Enter your LDAP password: ")

    # read sql query from file
    sqlfilename = "./my_sql_query.sql"
    f = open(sqlfilename)
    sql_string = f.read()
    print("SQL = " + sql_string)

    # set up connection through LDAP
    con = cx_Oracle.connect('{0}/{1}@**[DBservicename][.]**'.format(username, password)) 
      
    # create a cursor instance 
    cursor = con.cursor() 
      
    # run the query 
    cursor.execute(sql_string) 

    # print out metadata
    for column in cursor.description:
        print(column)
      
except cx_Oracle.DatabaseError as e: 
    print("There is a problem with Oracle", e) 
  
finally: 
    if cursor: 
        cursor.close() 
    if con: 
        con.close() 

```

I hope this post is helpful. If I missed anything, please let me know in the comments.

## References

cx_Oracle 8 Installation Document: https://cx-oracle.readthedocs.io/en/latest/user_guide/installation.html#install-oracle-client

Connecting Python to Oracle Databases with `cx_Oracle` and ldap: https://eikonomega.medium.com/connecting-to-oracle-database-with-cx-oracle-and-ldap-5da7925a305c
