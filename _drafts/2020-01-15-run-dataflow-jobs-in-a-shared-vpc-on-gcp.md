---
layout: post
published: false
title: Run Dataflow Jobs in a Shared VPC on GCP
date: '2019-01-14'
categories:
  - Google Cloud Platform
tags:
  - Dataflow
---

[Google Cloud Dataflow](https://cloud.google.com/dataflow/#benefits) is a fully managed unified stream and batch data processing service running Apache Beam on Google's infrastructures. With its serverless approach to resource provisioning and horizontal autoscaling, you have access to virtually unlimited capacity and optimized price-to-performance to solve your data processing challenges.
<!--more-->

[Shared Virtual Private Network (VPC)](https://cloud.google.com/vpc/docs/shared-vpc) allows an organization to connect resources from multiple projects to a common VPC network. This allows the resources to communicate with each other securely and efficiently using internal IP adresses from that network. When you use shared VPC, you designates a project as a **host project** and attach one or more **service projects** to it. The common VPC network shared accross host and service projects is called the **shared VPC network**. Share VPC is a good practice for Organization Admins keep centralized control over network resources, while delegating administrative resposibilities to Servcie Project Admins.

Because Google Cloud Dataflow service needs to use the network shared by the host project, there are some consigurations are neccessary to be set up on both host and serive projects to run the Dataflow jobs. This post sepecify the settings need to make and describes the steps to run a sample `WordCount` job with the Dataflow service.


# Table of Content

{:.no_toc}

* TOC
{:toc}

# Background Information
The host and service projects get involved are shown as below:



# Settings in Host Project



# Setting in Service Project




# Specifying Execution Paramters
