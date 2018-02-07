---
layout: post
published: false
title: Install Anaconda Python Distribution on Linux Server as Non-Sudo User
date: '2018-02-06'
categories:
  - Tutorial
tags:
  - Python
---

As a developer and data scientist, I often need to run Python scripts on Linux servers. The vast majority of CentOS/RHEL-based Linux servers use Python 2.6.6, while most of my Python application written in Python 3. In additoin, on most of the servers, I don't have the 'sudo' priviledge, so I need to install and configure Python 3 in my home directory. This post is a step-by-step instructions on installing [Anaconda distribution](https://docs.anaconda.com/) (Python 3) on a RHEL-based Linux server.

## Table of Content
{:.no_toc}

* TOC
{:toc}

## Check Installed Python Version
Chances are Python is already installed your Linux server, you can use following command to chech which version of Python you are woring with:

```
$ python -V
```
or
```
$ python --version
```