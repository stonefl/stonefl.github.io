---
layout: post
published: false
title: Deploy a Flask Application on an Azure VPS
tags:
  - Python
  - 'Azure '
  - Flask
  - Apache Web Server
categories:
  - Tutorial
---

[Flask](http://flask.pocoo.org/) is a micro framework for Python and based on Werkzeug and Jinja2 template engine for developing web applications. With the Azure VPS that has been configured in [last post](http://leifengblog.net/2017-11-14-how-to-install-apache-http-web-server-on-azure-ubuntu-virtual-machines/), in this post I will go through steps to deploy a flask application on the VPS.<!--more-->

## Step 1: Install WSGI

As we are going to use this VPS to host [Flask](http://flask.pocoo.org/) applications, in the first step, we need to install **[mod_wsgi](http://modwsgi.readthedocs.io/en/develop/index.html)**, which is a common interface between web servers and Flask applications, which allows Apache to talk to application and vice versa.
```
sudo apt-get update
sudo apt-get install libapache2-mod-wsgi   # for python 2.7
sudo apt-get install libapache2-mod-wsgi-py3  #for python 3
```
 
## Step 2: Install Python Environment and Flask

This step is to set up Python environment and dependent libraries for our Flask applications. After login to the VPS, you can check your python version and pip version through running following commands. You might have both python2.7 and python 3.x are pre-installed. 

```
python --version   # for python 2.7
python3 --version  # for python 3.x
pip --version    
pip3 --version
```

If `pip` is not currently installed yet, you can run following commands to install pip.
```
sudo apt-get update
sudo apt-get install python-pip  #for python 2.7
sudo apt-get install python3-pip #for python 3.x
```
### Python package management with pip

To install a package with pip, simply run:
```
pip install <package-name> # for python 2.7
pip3 install <package-name> # for python 3.x
```
To install Flask, simply run this:
```
pip install flask # for python 2.7
pip3 install flask # for python 3.x
```
After installing a set of packages, it is common courtesy in the Python community to create a list of packages that are required to run the program, so others can quickly install every thing required. This also has the added benefit that any new member of your project will be able to run your code quickly.

This list can be created with pip by running this:
```
pip freeze > requirements.txt
```

### Sandbox dependency with virtualenv
[Virtualenv](https://virtualenv.pypa.io/en/stable/) is a tool to create isolated Python environments. The secret to virtualenv is tricking your computer into looking for and installing packages in the project directory rather than in the main Python directory, which allows you to keep them completely separate.

You can install `virtualenv` for python 2.7 thorugh
```
sudo pip install virtualenv
```
For python 3, since `virtualenv` are bundled with python > 3.4. So you can run 
```
python3 -m venv <DIR>
```
to create a virtual environment for python 3.  Sometimes the `venv` is not pre-installed, then you might need to install the `python3-venv` package using following command.
```
sudo apt-get install python3-venv
```
To create the environment for your project, simply run: 
```
# cd to the project folder
virtualenv env # for python 2.7
python3 -m venv env # for python 3.x
```
The command tells `virtualenv` or `venv` to store all dependent packages into the `env` folder. Then you can use following commands to activate and deactivate the built virutal environment.
 ```
source  env/bin/activate
# you can use `pip` (no matter python 2 or 3) to install packages for the activaged environment
deactivate
```


## Deploy Flask Application

* Copy the project folder to `//var//www`. If get get a `permission denied` error, then you need to tak ownership of the `//var//www` directory for the Linux user that you're using, through running:
```
sudo chown -R <USERNAME> //var//www
```
* Copy the `.conf` file to `//etc//apache2//sites-available`
* Run following commands to start serve new Flask application;
```
sudo a2dissite 000-default.conf
sudo a2ensite hello.conf
sudo service apache2 reload
```
* If get error run following command to find what went wrong:
```
sudo tail –f //var//log//apache2//error.log
```



## References

* [Flask](http://flask.pocoo.org/)
