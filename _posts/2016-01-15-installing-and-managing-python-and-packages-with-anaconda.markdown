---
layout: post
author: stonefl
comments: true
date: '2016-01-15'
link: >-
  https://leifengtechblog.wordpress.com/2016/01/15/installing-and-managing-python-and-packages-with-anaconda/
slug: installing-and-managing-python-and-packages-with-anaconda
title: Installing and Managing Python and Packages with Anaconda
wordpress_id: 302
categories:
  - Python
published: true
tags:
  - Python
  - Anaconda
---

As more and more Python packages I need to install for my daily work and learn, I get tired of searching and installing individual packages, especially on my Window system, like what I did in [how to install scientific Python packages on Windows](https://wordpress.com/post/leifengtechblog.wordpress.com/183). I decide to give **Anaconda** (by [Continuum Analytics](https://www.continuum.io/)) a try, what it provides far exceed my expectation and I feel guilty did not try it earlier. <!--more-->

![capture.png]({{site.baseurl}}/img/post/capture.png)

Anaconda is a free, cross-platform, and easy-to-install all-in-one analytic/scientific Python platform. Anaconda not only comes with various packages that I would like to use, such as NumPy, SciPy, matplotlib, pandas, scikit-learn,  and Jupyter/IPython, but also provides more functionalities, like creating and managing environments, installing and updating packages, and so on.




In this post, I describe some basic knowledge on Anaconda I have learned through my experience. If you did not start to use it yet, I highly recommend you a try.


## Downloading and Installing


Installing Anaconda is as easy as 1-2-3:



	
  1. Go to Anaconda's download page ([http://continuum.io/downloads](http://continuum.io/downloads))

	
  2. download the right installer for your OS type (Window, OSX, Linux), OS version(32- or 64 bit), and Python version(2.7 or 3.5)

	
  3. Follow the instructions to install Anaconda


You might want to choose put Anaconda to your system path, so it will use Anaconda's Python as the default python distribution.

Anaconda comes with a package manager named **conda**, which lets you manage your Python distributions and install new packages.


## Managing Environments


Anaconda can help create different isolated Python environments. For example, you might use Python 3.5 as your default distribution, but sometimes you would switch to Python 2 for some rare cases.

Anaconda comes with a graphical launcher that you can use to  manage environments, install packages, start IPython, etc. You can find more details from [http://docs.continuum.io/anaconda-launcher/](http://docs.continuum.io/anaconda-launcher/)

All these stuff can be realized through **conda** command. For example, a new environment for Python 2 (named py2, with Python 2.7) can be created through following command:

** ` conda create -n py2 anaconda python=2.7 `**

Then the new environment can be activated through


**` activate py2`** on ** Windows**
**`source activate py2`** on **Linux or Mac OSX**


, and be deactivated by:

**` deactivate py2`** on ** Windows**
**`source deactivate py2`** on **Linux or Mac OSX**

NOTE: For Windows system, the activate and deactivate commands do not work in PowerShell, but work in cmd. Here is one potential solution, if you want to keep using your PowerShell: [Powershell activate and deactivate #626](https://github.com/conda/conda/issues/626)


## Common Commands


Here is a list of frequently used **conda** commands, and you can see a longer list at the [Conda cheet sheet.](https://leifengtechblog.files.wordpress.com/2016/01/conda-cheatsheet.pdf).






	
  * **`conda info`**: Displays information about current conda install.

	
  * **`conda help`**: Displays the list of conda commands and their help strings.

	
  * **`conda list`**: Lists all packages installed in the current environment.

	
  * **`conda env list`**: Displays the list of environments installed and the currently active one is marked by a star `*`.

	
  * **`conda serarch _somepackage_`**: search for a package to see if it is available.

	
  * **`conda install _somepackage_`**: Installs a Python package_._

	
  * **`conda install _somepackage_=0.7`**: Installs a specific version of a package.

	
  * **`conda update _somepackage_`**: Updates a Python package to the latest available version.

	
  * **`conda update anaconda`**: Updates all packages.

	
  * **`conda update conda`**: Updates conda itself.

	
  * **`conda update --all`**: Updates all packages.

	
  * **`conda remove somepackage`**: Uninstalls a Python package.

	
  * **`conda remove -n _myenv_ --all`**: Removes the environment named _`myenv`_.

	
  * **`conda clean -t`**: Removes the old tarballs that are left over after installation and updates.







If the **`conda install somepackage`** fails, you can try **`pip install somepackage`** instead, which uses the **PyPI** instead of Anaconda. Many scientific Anaconda packages are easier to install than the corresponding PyPI packages because they are pre-compiled for your platform. However, many packages are available on PyPI but not on Anaconda.














## A few references about Anaconda:

















	
  * Anaconda websit: [https://store.continuum.io/cshop/anaconda/](https://store.continuum.io/cshop/anaconda/)

	
  * Conda user cheet sheet [http://conda.pydata.org/docs/_downloads/conda-cheatsheet.pdf](http://conda.pydata.org/docs/_downloads/conda-cheatsheet.pdf)

	
  * List of Anaconda packages: [http://docs.continuum.io/anaconda/pkg-docs](http://docs.continuum.io/anaconda/pkg-docs)

	
  * Conda main page: [http://conda.io/](http://conda.io/)

	
  * Anaconda mailing list: [https://groups.google.com/a/continuum.io/forum/#!forum/anaconda](https://groups.google.com/a/continuum.io/forum/#!forum/anaconda)

	
  * Conda FAQ: [http://conda.pydata.org/docs/faq.html](http://conda.pydata.org/docs/faq.html)
