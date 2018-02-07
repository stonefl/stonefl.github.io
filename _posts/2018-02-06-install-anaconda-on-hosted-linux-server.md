---
layout: post
published: true
title: Install Python 3 Distribution on a Linux Server
date: '2018-02-06'
categories:
  - Tutorial
tags:
  - Python
---

As a developer and data scientist, I often need to run Python scripts on Linux servers. The vast majority of CentOS/RHEL-based Linux servers use Python 2.6.6, while most of my Python applications are written in Python 3. In additoin, on most of the servers, I don't have the `sudo` priviledge, so it needs a little trick to install Python 3 on those servers. 

This post is a step-by-step instructions on installing  Python 3.6 through both [Anaconda](https://docs.anaconda.com/) and [Python Gzipped source tarball file](https://www.python.org/downloads/release/python-364/) on a CentOS/RHEL-based  Linux server.<!--more-->

Anaconda is 

## Table of Content
{:.no_toc}

* TOC
{:toc}

## Check Python Version
Chances are Python is already installed on your Linux server, you can use following commands to check which version of Python has been installed:

```
$ python --version   
```
or
```
$ python -V
```
Most of the cases, Python 2.x is installed. Then you can install Python 3 by taking following steps.


## Instal through Anaconda

### Download Anaconda
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
or
```
$ sha256sum Anaconda3-5.0.1-Linux-x86_64.sh
```
You can check the output against the hashes available for your appropriate Anaconda version at the page of [Anaconda with Python 3 on 64-bit Linux](https://docs.anaconda.com/anaconda/install/hashes/lin-3-64). If the MD5 or SHA-256 hash that you generate does not match the one there, the file may not have downloaded completely, you might need to download it again and re-check.

### Install Anaconda

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

Press ENTER to continue and then continue press ENTER to review the license. Once you’re done reading the license, you’ll be prompted to agree to license terms:
```
Output
Do you approve the license terms? [yes|no] 
```

After type `yes`, you’ll be prompted to choose the location of the installation. 
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
You’ll receive the version number of the isntalled conda. Now the Anaconda is installed, you can check my another post([Managing Python Environments and Packages with Anaconda](http://leifengblog.net/blog/installing-and-managing-python-and-packages-with-anaconda/)) for setting and mangeing Python environments and packages.



## Install through Tarball File
You can install pure Python 3 distribution through following steps.

### Download Tarball File to Your Server
Go to the folder where you want to save the file (e.g./home/lf/) and run:
```
$ wget https://www.python.org/ftp/python/3.6.4/Python-3.6.4.tgz
```
It will download the tarbile from [Python's download page](https://www.python.org/downloads/release/python-364/).

### Verfiy (optional)
After download, you can verify the data integrity through running `MD5` hash
```
$ md5sum Python-3.6.4.tgz
```
You should compare the output to the result on the [download page](https://www.python.org/downloads/release/python-364/). As long as you get the same result, you are good to move ahead.

### Install

Decompress the file with the following command, which will create a directory `/home/lf/Python-3.6.4` and automatically copy all files into this directory. After decompression, the `Python-3.6.4.tgz` file can be deleted. 
```
$ tar xvzf Python-3.6.4.tgz
```
When the decompression is done, go into the created folder(`/home/lf/Python-3.6.4`) and install the new version of Python:
```
$ ./configure --prefix=$HOME/.local
```
This step sets up your configuration and makes files.

Then run the command:
```
$ make
```
and follow that up with:
```
$ make install
```
The last command will install two of the most useful Python utilities:

* [pip](https://pip.pypa.io/en/stable/): Python’s recommended tool for installing Python packages.
* [setuptools](https://pypi.python.org/pypi/setuptools): Enables you to download, build, install, and uninstall Python packages.

### Add Path to Evironment

Go back to your home folder and open the `.bashrc` file:
```
$ cd $HOME
$ nano .bashrc
```
with the editor open, add the following lines, and save the file:
```
# Python 3.6.4 
export PATH="$HOME/.local/bin:$PATH"
```
Run the following to get your environment up to date:
```
$ source ~/.bashrc
```

Now the Python 3 has been installed. You can verify the installation through running:
```
$python3 --version
```

Wait, why juse `python3` not just `python`? 
If you just run “python,” the executable will show the version number for the default Python for your version of Linux — not your newly installed version of Python. Confusing, I know. You will now have two versions of one language on your server.

The best way to handle this is to use Python’s virtualenv module to create a virtual Python environment. Inside this container-like environment, you can use your newer version of Python — such as Python 3.4.3 or 2.7.2. — without interfering with the preexisting Python.

### Create Virtual Python Environment


For more on the basics of using virtualenv, see Python Guide’s Virtual Environments. 


## References

[https://www.digitalocean.com/community/tutorials/how-to-install-the-anaconda-python-distribution-on-ubuntu-16-04](https://www.digitalocean.com/community/tutorials/how-to-install-the-anaconda-python-distribution-on-ubuntu-16-04)

[https://hostpresto.com/community/tutorials/how-to-install-anaconda-python-on-ubuntu-16-04/](https://hostpresto.com/community/tutorials/how-to-install-anaconda-python-on-ubuntu-16-04/)

[https://www.digitalocean.com/community/tutorial_series/how-to-install-and-set-up-a-local-programming-environment-for-python-3](https://www.digitalocean.com/community/tutorial_series/how-to-install-and-set-up-a-local-programming-environment-for-python-3)

[https://www.godaddy.com/garage/how-to-install-and-configure-python-on-a-hosted-server/](https://www.godaddy.com/garage/how-to-install-and-configure-python-on-a-hosted-server/)
