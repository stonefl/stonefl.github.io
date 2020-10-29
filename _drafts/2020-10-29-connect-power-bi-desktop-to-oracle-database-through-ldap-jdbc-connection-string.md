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

![private_sign]({{site.baseurl}}/img/post/sql_developer01.PNG)\


## References
Power BI Official Document
https://docs.microsoft.com/en-us/power-bi/connect-data/desktop-connect-oracle-database#installing-the-oracle-client

