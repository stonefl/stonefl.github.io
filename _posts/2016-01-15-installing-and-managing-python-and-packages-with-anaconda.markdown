---
layout: post
author: stonefl
comments: true
date: '2016-01-15'
link: >-
  https://leifengtechblog.wordpress.com/2016/01/15/installing-and-managing-python-and-packages-with-anaconda/
slug: installing-and-managing-python-and-packages-with-anaconda
title: Managing Python Environments and Packages with Anaconda
wordpress_id: 302
published: true
tags:
  - Python
  - Anaconda
categories:
  - Programming
---

As more and more Python packages I need to install for my daily work and learn, I get tired of searching and installing individual packages, especially on my Window system, like what I did in [how to install scientific Python packages on Windows](http://leifengblog.net/2015-11-24-how-to-install-numpy-scipy-scikit-learn-pandas-matplotlib-and-nltk-libraries-for-python-3-on-windows/). I decide to give **Anaconda** (by [Continuum Analytics](https://www.continuum.io/)) a try, what it provides far exceed my expectation and I feel guilty did not try it earlier. <!--more-->

![capture.png]({{site.baseurl}}/img/post/capture.png)

Anaconda is a free, cross-platform, and easy-to-install all-in-one analytic/scientific Python platform. Anaconda not only comes with various packages that I would like to use, such as NumPy, SciPy, matplotlib, pandas, scikit-learn, and Jupyter/IPython, but also provides more functionalities, like creating and managing environments, installing and updating packages, and so on.

In this post, I describe some basic knowledge on Anaconda I have learned through my experience. If you did not start to use it yet, I highly recommend you a try.


## Downloading and Installing

Installing Anaconda is as easy as 1-2-3:

1. Go to Anaconda's download page (<http://continuum.io/downloads>)

2. download the right installer for your OS type (Window, OSX, Linux), OS version(32- or 64 bit), and Python version(2.7 or 3.5)
	
3. Follow the instructions to install Anaconda

You might want to put Anaconda to your system path, so it will use Anaconda's Python as the default python distribution. On Windows, you are recommended not automatically add Anaconda to your system path, instead you can manually add **ANACONDA_HOME** with value of 'C:\User\\*your_user_name*\ AppData\Local\Continuum\anacondX' to the user varaibles and **%ANACONDA_HOME%; %ANACONDA_HOME%\Scripts; %ANACONDA_HOME%\ Library\bin;** to the user path variable.

Anaconda comes with a package manager named **conda**, which lets you manage your Python distributions and install new packages.


## Managing Environments

Anaconda can help create different isolated Python environments. For example, you might use Python 3.5 as your default distribution, but sometimes you would switch to Python 2 for some rare cases.

Anaconda comes with a graphical launcher that you can use to  manage environments, install packages, start IPython, etc. You can find more details from [http://docs.continuum.io/anaconda-launcher/](http://docs.continuum.io/anaconda-launcher/)

All these stuff can be realized through **conda** command. For example, a new environment for Python 2 (named py2, with Python 2.7) can be created through following command:

```
conda create -n py2 python=2.7
``` 

You can also specify the packages you want to install, for example
```
conda create -n myenv numpy pandas scipy python = 3.5
```

Then the new environment can be activated through

`activate py2` on **Windows**

`source activate py2` on **Linux or Mac OSX**


, and be deactivated by:

`deactivate py2` on **Windows**

`source deactivate py2` on **Linux or Mac OSX**

**NOTE:** For Windows system, the activate and deactivate commands do not work in PowerShell, but work in cmd. Here is one potential solution, if you want to keep using your PowerShell: [Powershell activate and deactivate #626](https://github.com/conda/conda/issues/626). You can also try another work around way:
1) type `cmd` in Powershell to switch to cmd line; 2) run activate or deactivate command; 3) type `powershell` to change back to Powershell.

## Use IPython Kernels for Different Environments

If you want to have multiple IPython kernels for different virtualenvs or conda environments, you will need to specify unique names for the kernelspecs.

Make sure you have ipykernel installed in your environment. If you are using `pip` to install `ipykernel` in a conda env, make sure `pip` is installed:
```
source activate myenv
conda install pip
conda install ipykernel # or pip install ipykernel
```

For example, using conda environments, install a `Python (myenv)` Kernel in a first environment:

```
source activate myenv
python -m ipykernel install --user --name myenv --display-name "Python (myenv)"
```

## Common Commands


Here is a list of frequently used **conda** commands, and you can see a longer list at the [Conda cheet sheet](http://conda.pydata.org/docs/_downloads/conda-cheatsheet.pdf).


* `conda info`: Displays information about current conda install.
	
* `conda help`: Displays the list of conda commands and their help strings.
	
* `conda list`: Lists all packages installed in the current environment.
	
* `conda env list`: Displays the list of environments installed and the currently active one is marked by a star `*`.

* `conda search _somepackage_`: search for a package to see if it is available.

* `conda install _somepackage_`: Installs a Python package_._

* `conda install _somepackage_=0.7`: Installs a specific version of a package.

* `conda update _somepackage_`: Updates a Python package to the latest available version.

* `conda update anaconda`: Updates all packages.

* `conda update conda`: Updates conda itself.

* `conda update --all`: Updates all packages.

* `conda remove somepackage`: Uninstalls a Python package.

* `conda remove -n _myenv_ --all`: Removes the environment named _`myenv`_.

* `conda clean -t`: Removes the old tarballs that are left over after installation and updates.


If the **`conda install somepackage`** fails, you can try **`pip install somepackage`** instead, which uses the **PyPI** instead of Anaconda. Many scientific Anaconda packages are easier to install than the corresponding PyPI packages because they are pre-compiled for your platform. However, many packages are available on PyPI but not on Anaconda.

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

You can now remove your entire Anaconda directory by entering the following command:
```
rm -rf ~/anaconda3 # on Linux
```
Finally, you can remove the PATH line from your ``.bashrc`` file that Anaconda added:
```
nano ~/.bashrc
```
Then delete or comment out the following lines:
```
# added by Anaconda3 installer
export PATH="/home/username/anaconda3/bin:$PATH"
```
When you’re done editing the file, type CTRL + X to exit and y to save changes. Then Anaconda is now removed from your server.


## A list of references about Anaconda:
	
* [Anaconda websit](https://store.continuum.io/cshop/anaconda/)

* [Conda user cheet sheet](http://conda.pydata.org/docs/_downloads/conda-cheatsheet.pdf)

* [List of Anaconda packages](http://docs.continuum.io/anaconda/pkg-docs)

* [Conda main page](http://conda.io/)

* [Anaconda mailing list](https://groups.google.com/a/continuum.io/forum/#!forum/anaconda)

* [Conda FAQ](http://conda.pydata.org/docs/faq.html)
