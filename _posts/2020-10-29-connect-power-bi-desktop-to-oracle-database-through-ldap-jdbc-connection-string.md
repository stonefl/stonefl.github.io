---
layout: post
published: true
title: >-
  Connect Power BI Desktop to Oracle Database through LDAP/JDBC Connection
  Strings
categories:
  - Database
tags:
  - Oracle
  - Power BI
thumbnail: /img/post/dashboard.jpg
---
Microsoft Power BI Desktop can connect to many data sources, one of the most popular datasources is Oracle Database. However, the missed steps on installation Oracle client and ambiguous specification of `ServerName/ServiceName` make the [Power BI's official document](https://docs.microsoft.com/en-us/power-bi/connect-data/desktop-connect-oracle-database#installing-the-oracle-client) hard to follow. This post aims to fill the gap with step-by-step instrucitons on installing and configuring an Oracle Data Access Client (ODAC) and how to get the connection information to an Oracle Database through the LDAP or JDBC connection strings.
<!--more-->

![private_sign]({{site.baseurl}}/img/post/dashboard.jpg)
Picture comes from ([https://unsplash.com/@goumbik](https://unsplash.com/photos/mcSDtbWXUZU))


## LDAP Connection in SQL Developer

There are serveral software clients can be used to connect to Oracle Database, [Oracel SQL Developer](https://www.oracle.com/database/technologies/appdev/sqldeveloper-landing.html) might be the most popular one. Authentication through a LDAP server is the most secure and popular way in SQL Developer to connect to an Oracle Database. The LDAP servers can be sepecified in both JDBC URL or LDAP connection. The following decribes the string formats in the two types of connections.

### Custom JDBC URL
![custom jdbc url]({{site.baseurl}}/img/post/sql_developer01.PNG)

The picture above shows an example of settings of Custom JDBC connection to an Oracle Database. The conncetion string in the **Custom JDBC URL** box usually has the format below:
```
jdbc:oracle:thin:@ldap://[ldapservername:port]/[DBservicename],cn=Oraclecontext,dc=domaincontext
```

### Transfer Custom JDBC URL to LDAP Connection
With the above custom JDBC URL, following the steps described below, you can create a new LDAP connection which can show the real `ServerName/ServiceName` information can be used by Power BI to connect to the Oracle Database:
* Create a new connection with a new **Name** in SQL Developer
* Fill in your **Username** and **Password**
* Select `LDAP` in the **Connection Type** drop-down list
* Put the `ldapservername:port` from the above custom JDBC URL into the **LDAP Server** field
* The **Context** should be loaded autoamatically
* Load the `DBservicename` as the **DB Service**
* **Test** the connection, if succeffuly, click the **Save** button.

After create the new connection, if you expand the left panel, you will find the **Connection Details** of the new LDAP connection, shown as the highlighted area below:
![connect_to_oracle_db]({{site.baseurl}}/img/post/connect-oracle-database_1.png)

The **Connection Details** has the following format:
```
[username]@//[servername]:[serverport]/[servicename]
```

## Install ODAC

### Step 1: Uninstall any existing version of ODAC on the machine.  
If you have installed the Xcopy version, to uninstall all ODAC products, execute the following command in the **Oracel Home** directory:
```
uninstall.bat all odac
```
If you have installed non-Xcopy version, you can use the Universal Installer. You can find it from:
**Start** -> **All programs** -> **Oracle - OraClient12Home1** ->**Oracle Installation Products**->**Universal Installer**.




## Connect to Oracle Database in Power BI Desktop
With the  above connection details information, you can take the following steps to conncet to the Oracle Database in Power BI Desktop:
* From the **Home** tab, select **Get Data**
* From the **Get Data** window that appears, select **More** (if necessary), select **Database** > **Oracle database**, and then select **Connect**

* You might get the warning message on recommended provider shown as below. Then click on the `Learn more` link to download and install ODAC. I have installed **64-bit ODAC 12.2c Release 1 (12.2.0.1.1) for Windows x64** using all default settings.
![connect_to_oracle_db]({{site.baseurl}}/img/post/connect-oracle-database_2.png)

* Copy the `[servername]:[serverport]/[servicename]` part from the above connection details in SQL Developer to the **Server** field shown as below, then click **OK**.
![connect_to_oracle_db]({{site.baseurl}}/img/post/connect-oracle-database_3.png)

**Note:**
The process described in this post is not the best way to connect to Oracel Database. You might notice that the `[servername]:[serverport]/[servicename]` in the connection details of the LDAP connection might change from time to time, because the Oracel server might be behind a network Load Balancer. In this case, you can refer to [this post](https://medium.com/@eikonomega/connecting-to-oracle-database-with-cx-oracle-and-ldap-5da7925a305c), [this post](http://technologydribble.info/2015/02/10/how-to-create-an-oracle-database-link-using-ldap-authentication/), and [this post](https://docs.oracle.com/cd/E11882_01/network.112/e10835/ldap.htm#NETRF011) for the settings of **ldap.ora** for an [Oracel client](https://www.oracle.com/database/technologies/install-odac-12c-122010.html).


## References
Power BI Official Document:
https://docs.microsoft.com/en-us/power-bi/connect-data/desktop-connect-oracle-database#installing-the-oracle-client

Making Database Connections from Oracle SQL Developer:
https://blogs.oracle.com/oraclemagazine/making-database-connections
