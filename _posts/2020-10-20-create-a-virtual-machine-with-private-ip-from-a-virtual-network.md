---
layout: post
published: true
title: >-
  Create a Virtual Machine with Private IP from a Virtual Network that's in a
  Different Subscription in Azure
date: '2020-10-20'
categories:
  - Azure
tags:
  - VM
  - Private IP
thumbnail: /img/post/private_sign.jpg
bigimg: /img/post/private_sign.jpg
---
In [previous post](https://leifengblog.net/blog/create-and-connect-to-azure-vm-under-company-proxy/) I described how to create a Linux Virtual Machine(VM) and connect to it through WindSCP on Windows 10 under a company proxy. However, it is not a best practice from security perspective. One of the best practices is to create a VM with private IP that comes from a dedicated Virtual Network (VNet). The VNet can be in the same Resource Group as the VM, but it can also be from different Resource Groups and even different Subscriptions. This post describes how to create a Linux VM with a Private IP in a VNet that comes from a different Subscription.

![private_sign]({{site.baseurl}}/img/post/private_sign.jpg)
Picture comes from ([https://unsplash.com/@timmossholder](https://unsplash.com/photos/0zRt0bQysMw))

## What is a Virtual Network(VNet)
VNet is a logically isolated network from each other in Azure. You can configure its IP address ranges, subnets, route tables, gateways, and security settings, much like a traditional network in a data center. Virtual Machines in the same VNet can access each other by default. VNet enables Azure resources, such as VMs, to securely communicate with each other, to the internet, and to on-premises networks.

## Settings in Azure Portal
If you prefer to use the Portal to create a VM, the following picture shows how to configure the **Networking** settings for the VM.
![azure_vm_private_ip]({{site.baseurl}}/img/post/azure_vm_private_ip.PNG)

Here are three important settings need to note:
* **Virtual network**: select an existing virutal network or create a new one.
* **Subnet**: select a subnet associated with the selected virtual network.
* **Public IP**: use a public IP address if you want to connect to the VM from outside internet. Choose `None` if you only need to communicate with the VM within the virtual network or your company networks.

## Create from Azure CLI
The [previous post](https://leifengblog.net/blog/create-and-connect-to-azure-vm-under-company-proxy/) described how to install Azure Cli and create SSH key pairs. If you haven't them yet, you can check out the post for assitance. It assumes that you have created a SSH private key file named `azure_vm.pub` that is located in `~/.ssh/`.

You can run the following commands to create a Linux VM with a private IP address assigned automatically from the `SUBNETID`. The `SUBNETID` is obtained through running the command of `az network vnet subnet show` and passing the names of VNet Resource Group, VNet, and Subnet. 

You can specify the VM name and admin username through changing the capitalized `VM-NAME` and `USERANME`, respectivley. 

You can specify a static private IP address with `--private-ip-address` parameter, such ass `--private-ip-address 192.168.1.101`. In this example, I didn't specify the private IP and let it assigned by the subnet automatically. 

You can also specify a static public IP address with the `--public-ip-address` parameter. The public ip has been set to empty in the following command, which means the VM has no public ip and cannot be accessed from the outside internet. 

```
export SUBNETID=$(az network vnet subnet show -g VNET-RESOURCE-GROUP-NAME --vnet-name VNET-NAME -n SUBNET-NAME -o tsv --query id)

az vm create \
  --resource-group RESOURCE-GROUP-NAME \
  --name VM-NAME \
  --image UbuntuLTS \
  --subnet "$SUBNETID" \
  --admin-username USERNAME \
  --public-ip-address "" \
  --location eastus2 \
  --ssh-key-values ~/.ssh/azure_vm.pub
```

**Note**: This command only works in Linux command environment. You have to use Windows Subsystem for Linux (WSL) on Windows 10, or you can run it in any Linux systems.

## References
https://docs.microsoft.com/en-us/azure/virtual-network/virtual-networks-overview

https://docs.microsoft.com/en-us/azure/virtual-network/virtual-networks-static-private-ip-arm-cli

## Credit
Title picture comes from ([https://unsplash.com/@timmossholder](https://unsplash.com/photos/0zRt0bQysMw))
