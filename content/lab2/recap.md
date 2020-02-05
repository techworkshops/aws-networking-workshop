---
title: "Recap"
menuTitle : "Recap"
date: 2019-12-20T10:22:08+05:30
weight : 3
---
Lets Recap what we have done so far:

- Create a logically isolated Virtual Private Cloud (VPC) that spans a region. 
- As per the 2-tier application requirements, we logically partioned the VPC into 4 subnets. 
- Familiarised on how to size a VPC and a subnet via CIDR blocks.
- Created an Internet Gateway to enable communication between VPC and Internet.
- Created NAT gateway to enable private subnet to make outbound calls to internet.
- Configured private and public subnet by using route tables.  
- Launched an EC2 instance in a public subnet.
- Controlled access to the EC2 instance by using security group.

Finally - dont forget to clean up the resources that we created previously.

The entire workshop is available as a downloadable cloud formation template for future reference download or launching into your account.

{{% button href="https://console.aws.amazon.com/cloudformation/home#/stacks/new?stackName=buildkite&templateURL=https://s3.amazonaws.com/my-great-stack.json" icon="fas fa-download" %}}Download Lab 1{{% /button %}}
{{% button href="https://console.aws.amazon.com/cloudformation/home#/stacks/new?stackName=buildkite&templateURL=https://s3.amazonaws.com/my-great-stack.json" icon="fas fa-rocket" %}}Launch Lab 1{{% /button %}}

TODO: Write the CFT