---
layout: post
published: false
title: Create a Virtual Machine with Private IP from a Virtual Network in Azure
date: '2020-10-20'
categories:
  - Azure
tags:
  - VM
  - Private IP
thumbnail: /img/post/private_sign.jpg
bigimg: /img/post/private_sign.jpg
---
In the [previous post](https://leifengblog.net/blog/create-and-connect-to-azure-vm-under-company-proxy/) I described how to a Linux Virtual Machine(VM) and connect to it through WindSCP on Windows 10 under a company proxy. However, it is not the best practice from security perspective. One of the best practices is to create a VM with private IP that comes from a dedicated Virtual Network (VNet) that can come from different Resource Groups even different subscriptions. This post describes how to create a Linux VM with a Private IP in a VNet.

## What is a Virtual Network(VNet)
Virtual Network is a logically isolated network from each other in Azure. You can configure their IP address ranges, subnets, route tables, gateways, and security settings, much like a traditional network in your data center. Virtual machines in the same virtual network can access each other by default. It also enables Azure resources, such as VM to securely communicate with each other, to the internet and to on-premises networks.

## Settings in Azure Portal
If you prefer to use protal to create a VM, the following picture shows how to 

## References
https://docs.microsoft.com/en-us/azure/virtual-network/virtual-networks-overview




## Credit
Title picture comes from ([https://unsplash.com/@timmossholder](https://unsplash.com/photos/0zRt0bQysMw))
