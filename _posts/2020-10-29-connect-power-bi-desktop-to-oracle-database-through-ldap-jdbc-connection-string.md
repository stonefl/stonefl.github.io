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
jdbc:oracle:thin:@ldap://[ldapservername:ldapport]/[DBservicename],[DomainContext]
```

### Transfer Custom JDBC URL to LDAP Connection
With the above custom JDBC URL, following the steps described below, you can create a new LDAP connection which can show the real `ServerName/ServiceName` information can be used by Power BI to connect to the Oracle Database:
* Create a new connection with a new **Name** in SQL Developer
* Fill in your **Username** and **Password**
* Select `LDAP` in the **Connection Type** drop-down list
* Put the `ldapservername:ldapport` from the above custom JDBC URL into the **LDAP Server** field
* The **Context** should be loaded autoamatically
* Load the `DBservicename` as the **DB Service**
* **Test** the connection, if succeffuly, click the **Save** button.

After create the new connection, if you expand the left panel, you will find the **Connection Details** of the new LDAP connection, shown as the highlighted area below:
![connect_to_oracle_db]({{site.baseurl}}/img/post/connect-oracle-database_1.png)

The **Connection Details** has the following format:
```
[username]@//[servername]:[serverport]/[servicename]
```

## Install and Configure ODAC

#### Step 1: Uninstall any existing version of ODAC  
If you have installed the Xcopy version, to uninstall all ODAC products, execute the following command in the **Oracel Home** directory:
```
uninstall.bat all odac
```
If you have installed non-Xcopy version, you can use the **Universal Installer** as Administrator. You can find it from:
**Start** -> **All programs** -> **Oracle - OraClient12Home1** ->**Oracle Installation Products**->**Universal Installer**.

Note: If none of above works, you can also delete the folder of the ODAC version number under `C:\app\client\` and folder of `C:\Program Files\Oracle` directly.

#### Step 2: Check Power BI Desktop Version
You can find the version information from **Power BI Desktop** -> **Help** -> **About**. The following is a screenshot of 64-bit version.
![powerbi-version]({{site.baseurl}}/img/post/powerbi-version.png)

#### Step 3: Download ODAC Installation File
The installation file can be downloaded from [ODAC download](https://www.oracle.com/database/technologies/odac-downloads.html) page. In my case, I have downloaded `ODAC122011_x64.zip` from the **64-bit ODAC 12.2c Release 1 (12.2.0.1.1) for Windows x64** section.

#### Step 4: Install ODAC
Unzip the downloaded file and double-click on the `setup.exe` in the unzipped folder to start the installation process:
* Choose your preferred language
![powerbi-install01]({{site.baseurl}}/img/post/powerbi-install01.PNG)

* Choose `Use Existing Windows User`. In my case, my username is `corp\<EMP_ID>` and password is my LDAP password.
![powerbi-install02]({{site.baseurl}}/img/post/powerbi-install02.PNG)

* Use the default **Oracle base** and **Software location**.
![powerbi-install03]({{site.baseurl}}/img/post/powerbi-install03.PNG)

* Use the default **Available Product Components**.
![powerbi-install04]({{site.baseurl}}/img/post/powerbi-install04.PNG)

* It is recommended to configure ODP.NET for machine-wide level
![powerbi-install05]({{site.baseurl}}/img/post/powerbi-install05.PNG)

* It is O.K. to leave the **DB Connection Configuration** fields empty, because we are going to use the LDAP configurations. You can also fill them with the corresponding information from the section **LDAP Connection in SQL Developer** as shown in the picture below.
![powerbi-install06]({{site.baseurl}}/img/post/powerbi-install06.PNG)

* If you get error for pre-requisite check on certain items, uncheck the boxes for it and proceed.
![powerbi-install07]({{site.baseurl}}/img/post/powerbi-install07.PNG)

* The remaining installation steps are pretty straight forward. The installation will take couple of minutes.

After installation, navigate to installation directory (Oracle home), which is the **Software location** in the step of **Specify Installation Location** above. Then go into **Network** > **Admin**.

#### Step 5: Configure Connection
* Create two files `ldap.ora` and `sqlnet.ora` if they are not generated automatically. 
* The content of file`ldap.ora` should be similar to the following: 

```
DIRECTORY_SERVERS = (oid.myinfo.domain.com:3060)
DIRECTORY_SERVER_TYPE =oid
DEFAULT_ADMIN_CONTEXT="cn=OracleContext, dc=DomainContext"
```

You need to update the **DIRECTORY_SERVERS** to your `[ldapservername:ldapport]` and **DEFAULT_ADMIN_CONTEXT** to your `[DomainContext]`.
* File `sqlnet.ora` should have the follwing content in it:

```
NAMES.DIRECTORY_PATH= (LDAP, TNSNAMES, EZCONNECT)
```

* If you updated the **DB Connection Configuration** fields during the installation, you will find the file `tnsnames.ora` should have the following content.

```
FDW =
   (DESCRIPTION =
    (ADDRESS = (PROTOCOL = TCP)(HOST = [servername])(PORT = [serverport]))
    (CONNECT_DATA =
      (SERVER = DEDICATED)
      (SERVICE_NAME = [DBservicename]) 
    )
  )
```

## Connect to Oracle Database in Power BI Desktop
With the ODAC installation and configurations, you can take the following steps to conncet to the Oracle Database in Power BI Desktop.
* From the **Home** tab, select **Get Data**
* From the **Get Data** window that appears, select **More** (if necessary), select **Database** > **Oracle database**, and then select **Connect**
* Put the `[DBservicename]` in the **Server** box. If the OID is created with only `OracleContext`, then you need to append a dot at the end of service name. For example, if the service name is **ABC_DEFG** and the OID is created only under `OracleContext`, then it should be specified as **ABC_DEFG.**. 
![connect_to_oracle_db]({{site.baseurl}}/img/post/connect-oracle-database_3.png)

**Note:** if `[DBservicename]`does not work, you can try to copy the `[servername]:[serverport]/[servicename]` from the above connection details in SQL Developer to the **Server** field.

* If asked, user the Database credentials to connect to the database.
![powerbi-install08]({{site.baseurl}}/img/post/powerbi-install08.PNG)





## References

https://docs.microsoft.com/en-us/power-bi/connect-data/desktop-connect-oracle-database#installing-the-oracle-client

https://blogs.oracle.com/oraclemagazine/making-database-connections

https://medium.com/@eikonomega/connecting-to-oracle-database-with-cx-oracle-and-ldap-5da7925a305c

http://technologydribble.info/2015/02/10/how-to-create-an-oracle-database-link-using-ldap-authentication/

https://docs.oracle.com/cd/E11882_01/network.112/e10835/ldap.htm#NETRF011

https://www.oracle.com/database/technologies/install-odac-12c-122010.html
