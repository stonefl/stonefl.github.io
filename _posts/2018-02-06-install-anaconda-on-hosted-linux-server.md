---
layout: post
published: true
title: Install Anaconda Python Distribution on Linux Server as Non-Sudo User
date: '2018-02-06'
categories:
  - Tutorial
tags:
  - Python
---

As a developer and data scientist, I often need to run Python scripts on Linux servers. The vast majority of CentOS/RHEL-based Linux servers use Python 2.6.6, while most of my Python applications are written in Python 3. In additoin, on most of the servers, I don't have the `sudo` priviledge, so I need to install and configure Python 3 in my home directory. This post is a step-by-step instructions on installing [Anaconda distribution](https://docs.anaconda.com/) for Python 3.6 version on a CentOS/RHEL-based  Linux server.<!--more-->

## Table of Content
{:.no_toc}

* TOC
{:toc}

## Check Python Version
Chances are Python is already installed on your Linux server, you can use following commands to check which version of Python has been installed:

```
$ python -version
```
Most of the cases, Python 2.x is installed. Then you can install Python 3 by taking following steps.


## Installing Anaconda

### Download
You can download the latest Anaconda installer from [Anaconda Download page](https://www.anaconda.com/download/#linux). At the time of writing, the latest version is 5.0.1 for Python 3.6.

From the folder where you want to save the installer, you can use `curl` to download the link that you copied from the Anaconda website:
```
$ curl -O https://repo.continuum.io/archive/Anaconda3-5.0.1-Linux-x86_64.sh
```
It will take a while to download.

### Verify(Optional)
Once the downloading process is done, you can verify the data integrity of the installer with `MD5` or `SHA-256`cryptographic hashes:
```
$ md5sum Anaconda3-5.0.1-Linux-x86_64.sh
```
```
$ sha256sum Anaconda3-5.0.1-Linux-x86_64.sh
```
You should check the output against the hashes available for your appropriate Anaconda version at the page of [Anaconda with Python 3 on 64-bit Linux](https://docs.anaconda.com/anaconda/install/hashes/lin-3-64). If the MD5 or SHA-256 hash that you generate does not match the one there, the file may not have downloaded completely. Please download it again and re-check.

### Install

Now you can run the script to install:
```
bash Anaconda3-5.0.1-Linux-x86_64.sh
```

You should see the following output:
```
Output

Welcome to Anaconda3 5.0.1 (by Continuum Analytics, Inc.)

In order to continue the installation process, please review the license
agreement.
Please, press ENTER to continue
```

Press ENTER to continue and then continue press ENTER to review the license. Once you’re done reading the license, you’ll be prompted to approve the license terms:
```
Output
Do you approve the license terms? [yes|no] 
```
Type `yes` to agree the licence terms.

Then you’ll be prompted to choose the location of the installation. 
```
Output
Anaconda3 will now be installed into this location:
/home/lf/anaconda3

  - Press ENTER to confirm the location
  - Press CTRL-C to abort the installation
  - Or specify a different location below
```
You can press ENTER to accept the default location, or specify a different location to modify it.The installation process will start copying files and installing required modules to your specified location. 

Once it’s complete you’ll receive the following output:
```
Output
...
installation finished.
Do you wish the installer to prepend the Anaconda3 install location
to PATH in your /home/sammy/.bashrc ? [yes|no]
[no] >>>
```
Type yes so that you can use the `conda` commandline. 

Next, run following activate the installation:
```
source ~/.bashrc
```
Once you are finished, you can verify the installation by running:
```
conda --version
```
You’ll receive the version number of the isntalled conda. Now that Anaconda is installed, you can check my another post([Managing Python Environments and Packages with Anaconda](http://leifengblog.net/blog/installing-and-managing-python-and-packages-with-anaconda/)) for setting and mangeing Python environments and packages.

## Uninstalling Anaconda
If for any reason you need to uninstall Anaconda, you should start with the `anaconda-clean` module:
```
conda install anaconda-clean
```
Once it is installed, you can run the following command to do the uninstallation:
```
anaconda-clean --yes
```
This will also create a backup folder called `.anaconda_backup` in your home directory:
```
Output
Backup directory: /home/lf/.anaconda_backup/2018-02-05T301831
```
You can now remove your entire Anaconda directory by entering the following command:
```
rm -rf ~/anaconda3
```
Finally, you can remove the PATH line from your ``.bashrc`` file that Anaconda added:
```
nano ~/.bashrc
```
Then delete or comment out the following lines:
```
# added by Anaconda3 5.0.1 installer
export PATH="/home/lf/anaconda3/bin:$PATH"
```
When you’re done editing the file, type CTRL + X to exit and y to save changes.

Anaconda is now removed from your server.
