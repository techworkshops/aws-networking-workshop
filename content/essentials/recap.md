---
title: "What we have Learnt So Far"
menuTitle : "Recap"
date: 2019-12-20T10:22:08+05:30
draft: true
weight : 3
---
Lets Recap what we have done so far: 

- Create a logically isolated Virtual Private Cloud (VPC) that spans a region. 
- As per the n-tier application requirements, we logically partioned the VPC into 4 subnets. 
- Familiarised on how to size a VPC and a subnet via CIDR blocks.       
- Created an Internet Gateway to enable communication between VPC and Internet.
- Created NAT gateway to enable private subnet to make outbound calls to internet. 
- Configured private and public subnet by using route tables.  
- Launched an EC2 instance in a public subnet. 
- Controlled access to the EC2 instance by using security group. 

The entire workshop is available as a cloud formation template in case you need it for future reference. 

Click on Launch Stack to deploy into your aws account. 
[![Launch Chapter 1](https://s3.amazonaws.com/cloudformation-examples/cloudformation-launch-stack.png)](https://console.aws.amazon.com/cloudformation/home#/stacks/new?stackName=buildkite&templateURL=https://s3.amazonaws.com/my-great-stack.json)
TODO: Write a CFT
