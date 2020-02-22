---
layout: post
published: false
title: Run Dataflow Jobs in a Shared VPC on GCP
date: '2019-01-14'
categories:
  - Google Cloud Platform
tags:
  - Dataflow
bigimg: /img/post/Google-Cloud-Logo.png
thumbnail: /img/post/Google-Cloud-Logo.png
---

[Google Cloud Dataflow](https://cloud.google.com/dataflow/#benefits) is a serverless unified stream and batch data processing service running Apache Beam. With its serverless approach to resource provisioning and horizontal autoscaling, you have access to virtually unlimited capacity and optimized price-to-performance to solve your data pipeline processing challenges.
<!--more-->

[Shared Virtual Private Network (VPC)](https://cloud.google.com/vpc/docs/shared-vpc) allows an organization to connect resources from multiple projects to a common VPC network. This allows the resources to communicate with each other securely and efficiently using internal IP adresses from that network. When you use shared VPC, you designates a project as a **host project** and attach one or more **service projects** to it. The common VPC network shared accross host and service projects is called **shared VPC network**. Shared VPC is a good practice for organization admins keep centralized control over network resources, while delegating administrative resposibilities to servcie project admins.

Because Google Cloud Dataflow service needs to use the network shared by the host project, there are some consigurations are neccessary to be set up on both host and serive projects to run the Dataflow jobs. This post describes the settings steps need to setup to run a sample `WordCount` job with the Dataflow service.


# Table of Content

{:.no_toc}

* TOC
{:toc}

# Orgnization and Shared VPC

The organization structure is shown as the following table. The Organization node(`leifengblog.net`) has two projects: `my-service-project` is the service project where the Dataflow program runs and `my-host-project` is the host project that hosts the shared VPC. 

![org_structure.JPG]({{site.baseurl}}/img/post/org_structure.JPG)

For the best practices, I have setup the following constraints in the `Organization Policies` page under the organization's `IAM & Admin` menu. 

|   Constraint   |   Configuration      |  Exaplanation |
| ------------- | -------------  |------------- |
| `Define allowed external IPs for VM instances` | Set `Policy values` to `Deny All` | All VM instances are not allowed to use external IP address |
| `Skip default network creation` | Pick `Customize` and turn on `Enforcement` | Don't create default network when create new project |

The VPC shared to the service project is shown in the following table. There are three custom subnets with `Private Google access` on.
![shared-vpc.JPG]({{site.baseurl}}/img/post/shared-vpc.JPG)

In addition, the following firewalls are applied to all instances in the shared VPC networks.

![shared-vpc.JPG]({{site.baseurl}}/img/post/firewall-rules.JPG)



# Settings on Host Project



# Setting in Service Project




# Specifying Execution Paramters
