---
layout: post
published: true
title: How to use pip behind a proxy
date: '2017-08-15'
categories:
  - Tips and Tricks
tags:
  - Python
  - Proxy
  - pip
---
We often need to use the python package manager `pip` to install a python package on my office computer that is behind a proxy. Without specifying the proxy info, it always pop up `Connection refused`errors. Following commands can be used to make 'pip install' work smoothly.

## On Windows
You can set up the proxy first through

`set https_proxy=https://[username:password@]proxyserver:port` and install the package
`pip install somepackage`

or

`pip install --proxy=https://[username:password@]proxyserver:port somepackage`

## On Linux
Set up the proxy fist through

`export https_proxy=https://[username:password@]proxyserver:port` and then
`pip install somepackage`

or

`sudo pip install --proxy=https://[username:password@]proxyserver:port somepackage`

