---
author: stonefl
comments: true
date: 2015-10-27 20:26:53+00:00
layout: post
link: https://leifengtechblog.wordpress.com/2015/10/27/install-and-run-jupyter-ipython-notebook-on-windows/
slug: install-and-run-jupyter-ipython-notebook-on-windows
title: Install and Run Jupyter (IPython) Notebook on Windows
wordpress_id: 145
categories:
- Programming Language
- Python
- Tips and Tricks
tags:
- IPython
- Jupyter Notebook
- Python
---

To install Jupyter Notebook, you will need Python installed on your system. I assume that, like me, you already installed the newest Python package on your Windows system and now you want to install and use the Jupyter Notebook.


## How to Install Jupyter Notebook





	
  * Add the scripts directory in your Python package where the 'pip.exe' and 'pip3.exe' located, in my case the path is 'C:\Python34\Scripts', to the PATH environment variables.

	
  * Run '`pip3 install jupyter`' in the command shell. Use pip instead of pip3 for legacy Python2. Note: if you are using the old `cmd.exe` shell, I strongly recommend you to switch to `Windows PowerShell,` which is integrated by default in Windows 7 and 8. The most common filesystem-related commands (like `pwd, cd, ls, cp, ps`, and so on) it has are the same ones in Unix.


The installation of Jupyter Notebook above will also install the IPython kernel which allows working on notebooks using the Python programming language.

	
  * If the IPython console has been installed correctly, you should be able to run it from the command shell with the '`ipython'` command.

	
  * Sometime it show a warning of readline service is not available. This is because the `pyreadline`, which is a dependency of IPython providing line-editing features, has not been installed in above installation process. You can run '`pip install pyreadline`' to install it.




## How to Run the Notebook





	
  1. Go to the notebook project directory and run '`jupyter notebook`' or '`ipython notebook`' in command shell. If you didn't select the project directory, the notebook web application will open the directory where you run the command.

	
  2. Use 'Ctrl + C' to stop any running server and shut down all kernels.


For detailed information on installation and configurations please go to [Jupyter Documentation](https://jupyter.readthedocs.org/en/latest/index.html).
