---
layout: post
published: false
title: How to Install Apache HTTP Web Server on Azure Ubuntu Virtual Machines
categories:
  - Web Application
tags:
  - Python
  - 'Azure '
  - Cloud Service
  - Flask
subtitle: Serving Python 3 Flask Application with WSGI
---

Apache HTTP Server is the most used web server software in the world and public cloud services, such as Amazon Web Services and Microsoft Azure, make setting up a Virtual Private Server(VPS) hosting web applications a lot easier than traditional way that using physical servers. As many tutorials on traditional web hosts are focusing on settings to run PHP and/or .NET applications, in this post I will go through the steps of installing and configuring Apache HTTP Web Server on an Azure Ubuntu Virtual Machine to host Flask Web applications writtern in Python 3. <!--more-->

## Set up Linux Virtual Machines on Azure
You can follow the steps from [Azure Linux Virtual Machines Quickstarts](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/) to create a virtual machine running Ubuntu. The quickstart also provide steps of installing a NGINX webserver on the virtual machine. 

One of the steps is to create SSH key pair, if you don't have an existing one. You can run following command in a Bash shell, e.g. Git Bash on Windows. Follow the on-screen directions to privide file path and name for the public key file. 
```
ssh-keygen -t rsa -b 2048
```

## Settings for Connection
After deloyment of virtual machine there are two things you need to set in order to connect to the virtual machine.
* Reset password through the **Reset password** tab on the left-hand menu
* Open port 80 for web traffic. Click **Networking** tab on the left-hand menu, and then **Add inbound port rule**, select type **http** from the **Service** dropbox.

You can run `ssh lei@xx.xxx.xxx.xxx` in your bash shell to connect to your virtual machine. You can also use WinSCP to connect to your virutal machine. You might need to set the proxy if you behind a proxy server. Note: there is no http:// in the proxy host name.

## Install Python Virtual Environment

After login to your virtual machine, you can check your python versions and pip version through running following commands. 

```
python --version
python3 --version
```
You might have both python2.7 and python 3.x pre-installed. 

If you want to use python 2.7, you have to check the pip version through running 
```
pip --version
```
If `pip` is not currently installed yet, you can run following commands to install pip for python 2.7.
```
sudo apt-get update
sudo apt-get install python-pip
```
You can install and use `virtualenv` for python 2.7 thorugh
```
sudo pip install virtualenv
virtualenv <DIR>
source <DIR>/bin/activate
```

If you want to use python 3, since both `pip` and `virtualenv` are bundled with python > 3.4. So you can run 
```
python3 -m pip install [package_to install]
```
to install packages. And run 
```
python3 -m venv <DIR>
source  <DIR>/bin/activate
```
to create and activate virtual environments for python 3.


 `python3 -m venv <DIR>` to create a virtual environment. You might need to install the python3-venv package using following command.
 ```
 sudo apt-get install python3-venv
 ```
 You can use following commands to activate and deactivate the built virutal environment.
 ```
source  <DIR>/bin/activate
deactivate
```
 

## References

* [Azure Linux Virtual Machines Quickstarts](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/)
