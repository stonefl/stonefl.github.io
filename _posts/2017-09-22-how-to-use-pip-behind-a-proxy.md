---
layout: post
published: true
title: How to Use pip behind a Proxy
date: '2017-08-15'
tags:
  - Python
  - Proxy
  - pip
categories:
  - Tutorial
---
I often need to use the python package manager `pip` to install a python package on my office computer that is behind a proxy. Without specifying the proxy info, it always pop up `Connection refused`errors. Following settings and commands can be used to make 'pip install' work smoothly.
<!--more-->

## On Windows
You can manually set up proxy environment variables through right-click on **This PC** (Windows 10) or **Computer** (Widnows 7) --> **Proporties** --> **Advanced system settings** --> **Environment variables** then add environment variables:

1. User variable(only for current login user):

    - Variable: `HTTP_PROXY`
    - Value: `"http://proxyserver:port"`
   and 
    - Variable: `HTTPS_PROXY`
    - Value: `https://proxyserver:port`
2. System variable(all users):

    - Variable: `HTTP_PROXY`
    - Value: `http://proxyserver:port`
   and 
    - Variable: `HTTPS_PROXY`
    - Value: `https://proxyserver:port`

You can also set up the proxy through comand lines:

~~~
set http_proxy=`http://[username:password@]proxyserver:port`
set https_proxy=`https://[username:password@]proxyserver:port`
~~~

After setting up proxies, then you can install packages through running:
~~~
pip install somepackage
~~~

Alternativelly, you can also specify proxy settings in the `pip` command:

~~~
pip install --proxy=`https://[username:password@]proxyserver:port` somepackage
~~~

## On Linux
Set up the proxy through

~~~
export https_proxy=`https://[username:password@]proxyserver:port`
~~~

and then install package:

~~~
pip install somepackage
~~~

or specify proxy in `pip` command:

~~~
sudo pip install --proxy=`https://[username:password@]proxyserver:port` somepackage
~~~
