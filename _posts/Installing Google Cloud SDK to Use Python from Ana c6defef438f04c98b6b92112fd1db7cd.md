
--
category: Google Cloud Platform
date: 2020/06/07
layout: post
published: true
tags: Cloud SDK
title: Installing Google Cloud SDK to Use Python from Anaconda
--
As a power user of GCP you definately need to use gcloud, gsutil and bq

You will need `gcloud` to login into and do a lot things on GCP. The following is the process you can follow to install Google Cloud SDK on your local computer.

Because the bundled python is 2.7, if you want to use the Python 3 from your Anaconda distribution, The following process is for you. The process has been tested on both Windows 10 and Ubuntu Linux systems.

### **1. Install Python**

Google Cloud SDK needs Python, so first thing you need to do is to make sure Python has been available. As Cloud SDK version 274.0.0, most of its components support Python 3.

If you are still using Python2, I highly recommend you to change now. If you have not used Anaconda yet, I also highly recommend you to try it out. You can follow this [post](http://leifengblog.net/blog/installing-and-managing-python-and-packages-with-anaconda/) to install and quick start Anaconda.

### **2. Set up `CLOUDSDK_PYTHON` Environmental Variable**

- If you are using Windows, add the following to your Environmental Variables:
    - Variable name: `CLOUDSDK_PYTHON`
    - Variable value: `path\to\anaconda3\python.exe`
- If you are using Linux or macOS, add the following line to the `.bashrc` file.

```
export CLOUDSDK_PYTHON="/home/username/anaconda3/bin/python"
```

and run `source .bashrc` to refressh your change.

### **3. Download and Install Google Cloud SDK**

- Download the appropriate archive compatible with your version from the [download page](https://cloud.google.com/sdk/docs/downloads-versioned-archives).
- Extract the contents of the file to any location on your file system.
- Add the Cloud SDK `bin` folder to your PATH environment:
    - On Windows:
        - run the command `.\google-cloud-sdk\install.bat` or
        - manually add `path\to\google-cloud-sdk\bin` to the `PATH` environmental variable.
    - On Linux or macOS:
        - run the command `./google-cloud-sdk/install.sh` or
        - manually add `export PATH="/path/to/google-cloud-sdk/bin:$PATH"` to `.bashrc`
- Run `gcloud init` to initialize the SDK.

### **4. Potential Error**

After finishing above three steps, you might have the error message shown below, if you run `gcloud --help` in CMD prompt on Windows.

This is causes by the Anaconda environment initialization. You need to run `activate base` to activate your base environment before run the gcloud commands:

![Installing%20Google%20Cloud%20SDK%20to%20Use%20Python%20from%20Ana%20c6defef438f04c98b6b92112fd1db7cd/gcloud_error.png](Installing%20Google%20Cloud%20SDK%20to%20Use%20Python%20from%20Ana%20c6defef438f04c98b6b92112fd1db7cd/gcloud_error.png)

[Installing Google Cloud SDK | Cloud SDK Documentation](https://cloud.google.com/sdk/install)

[Installing from versioned archives | Cloud SDK Documentation](https://cloud.google.com/sdk/docs/downloads-versioned-archives)