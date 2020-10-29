---
layout: post
published: false
title: >-
  Connect Power BI Desktop to Oracle Database through LDAP JDBC Connection
  String
categories:
  - Database
tags:
  - Oracle
  - Power BI
---
Microsoft Power BI Desktop can connect to multiple data sources, one of the most popular one is Oracle Database. There are serveral client software can be used to connect to Oracle Database, one of the most popular one might be the Oracel SQL Developer. Custom JDBC connection string with LDAP authentication is one of the multiple ways can be used in SQL Deverloper to connect to the Oracle Database. Intead of installing and configuring an Oracle Data Access Client (ODAC) that needs to be compatible with your Oracle Server described in Power BI's [official document](https://docs.microsoft.com/en-us/power-bi/connect-data/desktop-connect-oracle-database#installing-the-oracle-client), this post describes a way to figure out the ServerName/ServiceName that are required by Power BI through the custom JDBC connection string in SQL Developer.  

<!--more-->

![private_sign]({{site.baseurl}}/img/post/dashboard.jpg)
Picture comes from ([https://unsplash.com/@goumbik](https://unsplash.com/photos/mcSDtbWXUZU))

## Custom JDBC URL
![custom jdbc url]({{site.baseurl}}/img/post/sql_developer01.PNG)

The picture above shows an example of settings of a Custom JDBC connection to an Oracle Database. The URL/Conncetion string in the **Custom JDBC URL** box usually follows the format below:
```
jdbc:oracle:thin:@ldap://[ldapservername:port]/[DBservicename],cn=Oraclecontext,dc=domaincontext1,dc=domaincontext2
```
## Transfer Custom JDBC URL to LDAP Connection
With the custom JDBC URL, you can follow the steps below to create a new LDAP connection which can show the real ServerName/ServiceName information that is required by Power BI to connect to the Oracle Database:
* Create a new connection with a new name in SQL Developer
* Fill in your username and password
* Select `LDAP` in the **Connection Type** drop-down list
* Put the `ldapservername:port` from the above custom JDBC URL into the **LDAP Server** field
* The **Context** should be loaded autoamatically
* Load the `DBservicename` as the **DB Service**
* **Test** the connection, if succeffuly, click the **Save** button.

After create the new connection, you can expand the left panel, and you will find the **Connection Details** of the new LDAP connection, which has the following format:
```
[username]@//[servername]:[serverport]/[servicename]
```

## Connect to Oracle Database in Power BI Desktop
With the connection details information above, you can take the following steps to conncet to the Oracle Database:
* From the **Home** tab, select **Get Data**.
* From the **Get Data** window that appears, select **More** (if necessary), select **Database** > **Oracle database**, and then select **Connect**.
* Copy the `[servername]:[serverport]/[servicename]` part from the above connection details of the LDAP connection in SQL Developer to the **Server** field shown as below, then click **OK**.

![connect_to_oracle_db]({{site.baseurl}}/img/post/connect-oracle-database_3.png)

**Note:**
The process described in this post is not the best way to connect to Oracel Database. You might notice that the `[servername]:[serverport]/[servicename]` in the connection details of the LDAP connection, because the Oracel server might be behind a network Load Balancer. In this case, you can refer to [this post](https://medium.com/@eikonomega/connecting-to-oracle-database-with-cx-oracle-and-ldap-5da7925a305c) and [this post](http://technologydribble.info/2015/02/10/how-to-create-an-oracle-database-link-using-ldap-authentication/) for the settings of **ldap.ora** for the Oracel client.


## References
Power BI Official Document
https://docs.microsoft.com/en-us/power-bi/connect-data/desktop-connect-oracle-database#installing-the-oracle-client
Making Database Connections from Oracle SQL Developer
https://blogs.oracle.com/oraclemagazine/making-database-connections
