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

As a developer and data scientist, I often need to run Python scripts on Linux servers. The vast majority of CentOS/RHEL-based Linux servers use Python 2.6.6, while most of my Python application written in Python 3. In additoin, on most of the servers, I don't have the 'sudo' priviledge, so I need to install and configure Python 3 in my home directory. This post is a step-by-step instructions on installing [Anaconda distribution](https://docs.anaconda.com/) (Python 3.6 version) on a RHEL-based Linux server.

## Table of Content
{:.no_toc}

* TOC
{:toc}

## Check Installed Python Version
Chances are Python is already installed your Linux server, you can use following command to chech which version of Python you are woring with. 

```
$ python -V
```
or
```
$ python --version
```
Chances are Python 2.x has been installed. You can install Python 3 by taking following steps.


Installing Anaconda
The best way to install Anaconda is to download the latest Anaconda installer bash script, verify it, and then run it.

Find the latest version of Anaconda for Python 3 at the Anaconda Downloads page. At the time of writing, the latest version is 5.0.1, but you should use a later stable version if it is available.

Next, change to the /tmp directory on your server. This is a good directory to download ephemeral items, like the Anaconda bash script, which we won't need after running it.

cd /tmp
Use curl to download the link that you copied from the Anaconda website:

curl -O https://repo.continuum.io/archive/Anaconda3-5.0.1-Linux-x86_64.sh
We can now verify the data integrity of the installer with cryptographic hash verification through the SHA-256 checksum. We’ll use the sha256sum command along with the filename of the script:

sha256sum Anaconda3-5.0.1-Linux-x86_64.sh
You’ll receive output that looks similar to this:

Output
55e4db1919f49c92d5abbf27a4be5986ae157f074bf9f8238963cd4582a4068a  Anaconda3-5.0.1-Linux-x86_64.sh
You should check the output against the hashes available at the Anaconda with Python 3 on 64-bit Linux page for your appropriate Anaconda version. As long as your output matches the hash displayed in the sha2561 row then you’re good to go.

Now we can run the script:

bash Anaconda3-5.0.1-Linux-x86_64.sh
You’ll receive the following output:

Output

Welcome to Anaconda3 5.0.1 (by Continuum Analytics, Inc.)

In order to continue the installation process, please review the license
agreement.
Please, press ENTER to continue
Press ENTER to continue and then press ENTER to read through the license. Once you’re done reading the license, you’ll be prompted to approve the license terms:

Output
Do you approve the license terms? [yes|no]
As long as you agree, type yes.

At this point, you’ll be prompted to choose the location of the installation. You can press ENTER to accept the default location, or specify a different location to modify it.

Output
Anaconda3 will now be installed into this location:
/home/sammy/anaconda3

  - Press ENTER to confirm the location
  - Press CTRL-C to abort the installation
  - Or specify a different location below

[/home/sammy/anaconda3] >>> 
The installation process will continue, it may take some time.

Once it’s complete you’ll receive the following output:

Output
...
installation finished.
Do you wish the installer to prepend the Anaconda3 install location
to PATH in your /home/sammy/.bashrc ? [yes|no]
[no] >>> 
Type yes so that you can use the conda command. You’ll next see the following output:

Output
Prepending PATH=/home/sammy/anaconda3/bin to PATH in /home/sammy/.bashrc
A backup will be made to: /home/sammy/.bashrc-anaconda3.bak
...
In order to activate the installation, you should source the ~/.bashrc file:

source ~/.bashrc
Once you have done that, you can verify your install by making use of the conda command, for example with list:

conda list
You’ll receive output of all the packages you have available through the Anaconda installation:

Output
# packages in environment at /home/sammy/anaconda3:
#
_ipyw_jlab_nb_ext_conf    0.1.0            py36he11e457_0  
alabaster                 0.7.10           py36h306e16b_0  
anaconda                  5.0.1            py36hd30a520_1
...
Now that Anaconda is installed, we can go on to setting up Anaconda environments.

