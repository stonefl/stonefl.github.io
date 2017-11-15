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
You can follow the steps from [Azure Linux Virtual Machines Quickstarts](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/) to create a virtual machine running Ubuntu. The quickstart also provide steps of installing a NGINX webserver on the virtual machine. The steps of creating a virtual machine through Azure portal can be summarized below:

* **Step 1:** Create SSH key pair, if you don't have an existing one, through running following command in a Bash shell. You can use Git Bash on Windows. Follow the on-screen directions to privide file path and name for the public key file. 
```
ssh-keygen -t rsa -b 2048
```



![Create VM through Azure Portal]({{site.baseurl}}/img/post/capture.png/image/post/create-vm-portal-basic-blade.png  "Hadoop Ecosystem")





## References

* [Azure Linux Virtual Machines Quickstarts](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/)
