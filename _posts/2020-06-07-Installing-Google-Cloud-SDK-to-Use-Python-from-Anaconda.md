---
layout: post
published: true
title: Installing Google Cloud SDK to Use Python from Anaconda
date: '2020-06-07'
categories:
  - Google Cloud Platform
tags:
  - Cloud SDK
---


As a power user, you definately need to use `gcloud`, `gsutil` and `bq` commands to work with Google Cloud Platform, which means you need to install Google Cloud SDK on your local computer. You can install the Google Cloud SDK through many options, including versioned archives, installer, apt-get/yum for Linux distro, and even Docker image. This post describes the process of installing SDK through versioned archive that have already installed Python through Anaconda, which has been tested on both Windows 10 and Ubuntu 18.04 Linux operating systems.
<!--more-->

Installing through versioned archives might be the best way for non-interactive installation of a specific version of the Cloud SDK. Each of the versioned archive has a self-contained Cloud SDK packages in a directory that can be copied to any location on your file system. Thus you don't need to run any installer on your system.

Google Cloud SDK needs Python, however, its bundled Python package is still 2.7 and, since version 274.0.0, most of the Cloud SDK components already switch to Python 3. In order to use existing Python on your systems, especially, if you have already installed Python through Anaconda and want the Cloud SDK to use it, you need the process described in this post to make things work.

## 1. Install Python

If you are still using Python2, I highly recommend you to change to Python3 now. If you have not used Anaconda yet, I also highly recommend you to try it out. You can follow this [post](http://leifengblog.net/blog/installing-and-managing-python-and-packages-with-anaconda/) to install and quick start Anaconda.

## 2. Set up `CLOUDSDK_PYTHON` Environmental Variable

- If you are using Windows, add the following  variables to your **Environmental Variables**:
    - Variable name: `CLOUDSDK_PYTHON`
    - Variable value: `path\to\anaconda3\python.exe`
- If you are using Linux or macOS, add the following line to the `.bashrc` file.

```
export CLOUDSDK_PYTHON="/home/username/anaconda3/bin/python"
```

and don't froget to run `source .bashrc` to refressh your change.

## 3. Download and Install Google Cloud SDK

- Download the appropriate archive compatible with your version from the [download page](https://cloud.google.com/sdk/docs/downloads-versioned-archives).
- Extract the contents of the file to any location on your file system.
- Add the Cloud SDK `bin` folder to your PATH environment:
    - On Windows:
        - run the command `.\google-cloud-sdk\install.bat` **or**
        - manually add `path\to\google-cloud-sdk\bin` to the `PATH` environmental variable.
    - On Linux or macOS:
        - run the command `./google-cloud-sdk/install.sh` **or**
        - manually add `export PATH="/path/to/google-cloud-sdk/bin:$PATH"` to `.bashrc`
- Run `gcloud init` to initialize the SDK.

## 4. Potential Error

After finishing above three steps, you run `gcloud --help` to make sure everything works. You might see the error message as shown below:

![gcloud_error.png]({{site.baseurl}}/img/post/gcloud_error.png)


This is causes by the Anaconda environment initialization. You need to run `activate base` to activate your base environment before run the gcloud commands.


### Reference

[Installing from versioned archives](https://cloud.google.com/sdk/docs/downloads-versioned-archives)

[Installing Google Cloud SDK](https://cloud.google.com/sdk/install)
