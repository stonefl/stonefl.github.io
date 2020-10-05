---
layout: post
published: true
title: Create and Connect to Azure VM through WinSCP/PuTTY
date: '2020-10-01'
categories:
  - Azure
tags:
  - VM
  - SSH
  - Proxy
---
To learn Microsoft Azure Virtual Machine, the first thing you want to try might be to create a VM and connect to it. If you follow the steps described in Microsoft's [official quickstart document](https://docs.microsoft.com/en-us/azure/virtual-machines/windows/quick-create-cli), you most likely fail to connect to it, especially when you are under a company proxy. This post decribes the step-by-step process I performed to create a Linux VM and connect to it through WindSCP on Windows 10 under a company proxy. 

<!--more-->
![https://unsplash.com/photos/0qvBNep1Y04]({{site.baseurl}}/img/post/computer.jfif)
Picture from ([https://unsplash.com/@casparrubin](https://unsplash.com/photos/0qvBNep1Y04))

## Install Azure ClI
You can create a VM easily with the Azure Portal, but the Azure CLI would make your life easier. Installing Azure CLI on Windows is pretty simply and straightforward. You can simply follow the steps described in the document of [Install Azure CLI on Windows](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli-windows?tabs=azure-cli) to install the Azure CLI through downloading the Microsoft Installer(MSI) or Powershell command.

After installing, you can run `az login` to log into your azure account.
   
## Create SSH Key Pairs
SSH keys are going to be used for security connection from your WinSCP/PuTTY to the Azure VM. I usually run the command `ssh-keygen` through Git Bash on Windows, but it seems that Windows most-recent updates caused all `ssh` related commands in Git Bash stop working. I ran the following command in PowerShell to generate the SSH Key Pairs. Feel free to change the capitalized `USERANME` in the command, I always make it the same to the username I will use in the VM that is going to be created next.
```powershell
ssh-keygen -t rsa -b 4096 -C "USERNAME" -f $HOME/.ssh/azure_vm
```
You will be prompted to provide a passphrase, but you can keep it empty. If it runs successfully, you will get a private file(azure_vm) and a public key file (azure_vm.pub). Of course, you can change it to different file names intead of using _azurevm_ here.

## Create a Linux VM
You can run the following command to create a Linux VM with the ssh key file you created above. You can specify the VM name and admin username through changing the capitalized `VM-NAME` and `USERANME`, respectivley. 

```
az vm create \
  --resource-group RESOURCE-GROUP-NAME \
  --name VM-NAME \
  --image UbuntuLTS \
  --admin-username USERNAME \
  --ssh-key-values ~/.ssh/azure_vm.pub
```
Note, above command assumed that you have already created a resource group, if not, you can create one through the following command:
```
az group create --name myResourceGroup --location eastus
```
It might take a few minutes to create the VM. Once create successfully, you can see the created VM in the Azure Portal.

## Connect to VM under Proxy

If you are using Windows and under a compay proxy, WinSCP/PuTTY are best choices to connect to the remote VM and both of them have built-in support for tunneling through a HTTP proxy. This post describes the settings in WinSCP, which is the closely cooperate with PuTTY SSH client. So the instructions here are also applicable to PuTTY. You can download and install both WinSCP and PuTTY through this [link](https://winscp.net/eng/downloads.php).

To connect to the VM instance through WinSCP, start WinSCP, and Login dialog will appear. On the dialog:

* Make sure **New site** node is selected.
![WinSCP_newsite]({{site.baseurl}}/img/post/Winscp_newsite.PNG)
* On the **New site** node, make sure SFTP protocol is selected.
* Enter **Host name** with the public IP address of the created VM.
* Enter **User name** with the admin username when you create the VM.
* Click the **Advanced...** button to set up a public key authentication.
* Select **Authentication** under **SSH**, click the **...** to browse the **private file path**.
![WinSCP_authentication]({{site.baseurl}}/img/post/Winscp_authentication.PNG)
* Select the `azure_vm` file created from the command of `ssh-keygen`
* Select `OK` when it prompts to change OpenSSH private key format to PuTTY private key format.
* Save the transfered `.ppk` file to the `.ssh` folder.
* Select **Proxy** under **Connection** node.
![WinSCP_proxy]({{site.baseurl}}/img/post/Winscp_proxy.PNG)
* Enter **Proxy host name**, **Port number**, if applicable, enter **User name** and **Password**
* Save your site settings using the **Save** button.
* Login using the **Login** button.

   

## Reference
[Install Azure CLI for Windows](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli-windows?tabs=azure-cli)

[Quickstart - Create a Linux VM with Azure CLI](https://docs.microsoft.com/en-us/azure/virtual-machines/windows/quick-create-cli)

[SSH suddenly stopped working in git-bash on Windows 10](https://superuser.com/questions/1496843/ssh-suddenly-stopped-working-in-git-bash-on-windows-10)
