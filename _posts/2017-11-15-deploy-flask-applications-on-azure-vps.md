---
layout: post
published: true
title: Deploy a Flask Application on an Azure Virtual Machine
tags:
  - Python
  - 'Azure '
  - Flask
  - Apache Web Server
categories:
  - Tutorial
---

[Flask](http://flask.pocoo.org/) is a micro framework for Python and based on Werkzeug and Jinja2 template engine for developing web applications. With the Azure VPS that has been configured in [last post](http://leifengblog.net/blog/how-to-install-apache-http-web-server-on-azure-ubuntu-virtual-machines/), in this post I will go through steps to deploy a flask application on the VPS.<!--more-->
## Table of Content
{:.no_toc}

* TOC
{:toc}

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
There are 2 ways to do the package management, I personally prefere the second way:

### Way 1: Python package management with pip

To install a package with pip, simply run:
```
pip install <package-name> # for python 2.7
pip3 install <package-name> # for python 3.x
```
for example, to install Flask, simply run this:
```
pip install --user flask # for python 2.7
pip3 install --user flask # for python 3.x
```

### Way 2: Manage dependency with virtualenv
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
The command tells `virtualenv` or `venv` to store all dependent packages into the `env` folder. 

Then you can use following commands to activate and deactivate the built virutal environment.
 ```
source  env/bin/activate  # to activate environment
deactivate # to deactiate current environment
```
After activating an evironment, you can use `pip` (no matter python 2 or 3) to install packages for the activated environment, for example,
```
pip install --user flask
```
After installing a set of packages, it is common courtesy in the Python community to create a list of packages that are required to run the program, so others can quickly install every thing required. This also has the added benefit that any new member of your project will be able to run your code quickly.

This list can be created with pip by running:
```
pip freeze > requirements.txt
```

## Step 3: Deploy Flask Application

Built a directory of a hello-world Flask application using the structure looks something like:
~~~
|-----helloworld
|--------helloworld.py
|--------hello.wsgi
|--------hello.conf
|--------env
|-----------requirements.txt
~~~

The `helloworld.py` reads as:
```python
from flask import Flask
app = Flask(__name__)

@app.route('/')
def hello_world():
    return 'Hello, World!'
```

The content of `hello.wsgi` is:
```python
import sys
sys.path.insert(0, "/var/www/helloworld")
from helloworld import app as application
```

And the `hello.conf` looks like:
```python
<VirtualHost *>
    ServerName example.com
    WSGIScriptAlias / /var/www/helloworld/hello.wsgi
    WSGIDaemonProcess hello python-home=/var/www/helloworld/env
    <Directory /var/www/helloworld>
       WSGIProcessGroup hello
       WSGIApplicationGroup %{GLOBAL}
        Order deny,allow
        Allow from all
    </Directory>
</VirtualHost>
```


* Copy the project folder to `/var/www` on the VPS. If get get a `permission denied` error, then you need to tak ownership of the `/var/www` directory for the Linux user that you're using, through running:
```
sudo adduser <username> www-data
sudo chown -R www-data: www-data /var/www
sudo chmod -R g+rwX /var/www

```
* Build an evironment using instructions in Step 2 and activate the env. Then move to the env folder and install required packages through running:
```
pip install -r requirements.txt
```
* Copy `hello.conf` to `/etc/apache2/sites-available` 
* Run following commands to start serve new Flask application;
```
sudo a2dissite 000-default.conf
sudo a2ensite hello.conf
sudo service apache2 reload
```

If get get any errors run following command to find what went wrong:
```
sudo tail –f /var/log/apache2/error.log
```



## References

* [Flask](http://flask.pocoo.org/)
* [Virtualenv](https://virtualenv.pypa.io/en/stable/)
