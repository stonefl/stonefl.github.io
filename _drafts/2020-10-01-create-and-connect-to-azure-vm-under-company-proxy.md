---
layout: post
published: false
title: How to Create and Connect to Azure VM through WinSCP/Putty
date: '2020-10-01'
categories:
  - Azure
tags:
  - VM
  - SSH
  - Proxy
---
To learn Microsoft Azure, the first thing you might want to try is to create a VM and connect to it. If you follow the steps described in its official [quickstart document](https://docs.microsoft.com/en-us/azure/virtual-machines/windows/quick-create-cli), especially if you are under a company proxy. This post decribes the step-by-step process I used to create a Linux VM and connect to it through WindSCP on Windows 10 under a company proxy. 
<!--more-->

## Install Azure ClI
You can create a VM easily with the Portal, but the Azure CLI would make your life easier. Installing Azure CLI on Windows is pretty simply and straightforward. You can simply follow the steps described in the document of [Install Azure CLI on Windows](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli-windows?tabs=azure-cli) to install the Azure CLI through downloading the Microsoft Installer(MSI) or through Powershell command.
   
## Create SSH Key Pairs
SSH keys are going to be used for security connection from your WinSCP/Putty to the Azure VM. I usually use the command `ssh-keygen` through Git Bash on Windows, but it is seems that the Windows most recent updates caused all `ssh` related commands in Git Bash stop working. I used `cmd` run the following command to generate the SSH Key Pairs:
```cmd

```

3. Create VM

4. Connect to VM through Proxy
   Set proxy in WinSCP

## Reference
[Install Azure CLI for Windows](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli-windows?tabs=azure-cli)

[Quickstart - Create a Linux VM with Azure CLI](https://docs.microsoft.com/en-us/azure/virtual-machines/windows/quick-create-cli)

[SSH suddenly stopped working in git-bash on Windows 10](https://superuser.com/questions/1496843/ssh-suddenly-stopped-working-in-git-bash-on-windows-10)
