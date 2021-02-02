---
layout: post
published: false
title: Connect to Oracle Database with Python cx_Oracle through LDAP in Ubuntu
thumbnail: /img/post/mylaptop.jpg
date: '2021-01-31'
categories:
  - Programming
tags:
  - Python
  - Oracle
---
Configuration of cx_Oracle for Python to connect to remote Oracle Database is not trivial. To connect to remote Oracle Database in Python through LDAP authentication, you need to cx_Oracle and Oracle Instant Client libraries, as well as settings in the Oracle Client. This post describes the processes I followed to set up the connection to an Oracle Database on-premises in Python on a Ubuntu 18.04 LTS Virtual Machine on Microsoft Azure. 

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


## References

cx_Oracle 8 Installation Document: https://cx-oracle.readthedocs.io/en/latest/user_guide/installation.html#install-oracle-client



Enter text in [Markdown](http://daringfireball.net/projects/markdown/). Use the toolbar above, or click the **?** button for formatting help.
