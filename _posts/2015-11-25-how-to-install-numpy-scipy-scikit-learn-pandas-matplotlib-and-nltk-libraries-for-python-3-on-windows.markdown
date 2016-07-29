---
author: stonefl
comments: true
date: 2015-11-25 04:05:06+00:00
layout: post
link: https://leifengtechblog.wordpress.com/2015/11/24/how-to-install-numpy-scipy-scikit-learn-pandas-matplotlib-and-nltk-libraries-for-python-3-on-windows/
slug: how-to-install-numpy-scipy-scikit-learn-pandas-matplotlib-and-nltk-libraries-for-python-3-on-windows
title: How to Install Numpy, SciPy, Scikit-learn, Pandas, Matplotlib, and NLTK libraries
  for Python 3 on Windows
wordpress_id: 183
categories:
- Python
- Tips and Tricks
tags:
- Matplotlib
- NLTK
- NumPy
- Pandas
- Python
- Scikit
- SciPy
---

NumPy, SciPy, Pandas, and Matplotlib are fundamental scientific computing and visualization packages with Python. Scikit-learn is a simple and efficient package for data mining and analysis in Python. NLTK (the Natural Language Toolkit) is a leading platform for building Python programs to work with human language data. However, if you are using Python on Windows, it seems not easy to install these packages. Thanks to [Christoph Gohlke](http://www.lfd.uci.edu/~gohlke/), who provides the [non-official Python extension packages for Windows](http://www.lfd.uci.edu/~gohlke/pythonlibs/). With these unofficial packages, there is a simple way to install these libraries on Windows.

For clarity, I'm using Python 3.4.3 on 64-bit Windows 7. The steps described below would also work for 32-bit. Please note, after installed Python, I added the 'Scripts' directory in Python package where the 'pip.exe' and 'pip3.exe' located, in my case the path is 'C:\Python34\Scripts', to the PATH environment variables. This step makes my life easier, because I don't need to navigate to the scripts directory anytime I run 'pip' or 'python'.


## Install NumPy, SciPy, Pandas, and Matplotlib


The steps of installation of Numpy, SciPy, Pandas, and Matplotlib are the same. Here I take NumPy as an example:




	
    1. Download appropriate wheel file, in my case, for numpy, it is "numpy-1.10.1+mkl-cp34-none-win_amd64.whl" from [the unofficial extension packages site](http://www.lfd.uci.edu/~gohlke/pythonlibs/)

	
    2. On the command line, navigate to the directory where you saved the wheel file

	
    3. Run `pip install numpy-1.10.1+mkl-cp34-none-win_amd64.whl`

	
    4. To verify, start python and run




[code language="python"] >>> import numpy  
>>> numpy.__version__
[/code]



## Install Scikit-learn


With a working installation of Numpy and Scipy, it is easy to install scikit-learn through running: `pip install -U scikit-learn`


## Install NLTK


To install NLTK we need to install the Pyyaml package. Follow the steps for installing Numpy above to install Pyyaml first and then NLTK.


## References


https://www.codementor.io/numpy/tutorial/installing-numpy-64-bit-windows

http://scikit-learn.org/stable/install.html

