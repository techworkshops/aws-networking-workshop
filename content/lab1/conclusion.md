---
title: "Conclusion"
menuTitle : "Conclusion"
date: 2019-12-20T10:22:08+05:30
weight : 3
---
### What we have built so far

- Created a logically isolated Virtual Private Cloud (VPC) that spans a region.
- As per the 2-tier application requirements, we logically partioned the VPC into 4 subnets.
- Familiarised on how to size a VPC and a subnet via CIDR blocks.
- Created an Internet Gateway to enable communication between VPC and Internet.
- Created NAT gateway to enable private subnet to make outbound calls to internet.
- Configured private and public subnet by using route tables.  
- Launched an EC2 instance in a public subnet.
- Controlled access to the EC2 instance by using security group.

Finally - dont forget to clean up the resources that we created previously.

#### ❗ Cleanup ❗

To prevent your account from accruing additional charges, you should remove any resources that are no longer needed

- Download and save a copy of the CloudFormation Template created in step:9. This will help you to recreate the entire VPC automatically
- Terminate the EC2 instances - 'bastion host' and 'secure host'
- Delete the Security Groups
- Delete the NACL rules
- Disassociate and Delete the Routetables
- Delete the NAT Gateways
- Delete the ElasticIPs
- Delete the Subnets - both the public and both the private subnets
- Detach and delete the InternetGateway
- Delete the VPC

The entire workshop is available as a downloadable cloud formation template for future reference download or launching into your account.

{{% button href="https://console.aws.amazon.com/cloudformation/home#/stacks/new?stackName=buildkite&templateURL=https://s3.amazonaws.com/my-great-stack.json" icon="fas fa-download" %}}Download Lab 1{{% /button %}}
{{% button href="https://console.aws.amazon.com/cloudformation/home#/stacks/new?stackName=buildkite&templateURL=https://s3.amazonaws.com/my-great-stack.json" icon="fas fa-rocket" %}}Launch Lab 1{{% /button %}}

TODO: Write the CFT