---
title: "Lab Description"
date: 2019-12-20T10:22:08+05:30
draft: true
weight: 1
---

#### Overview

In this lab, you will learn how to build a Virtual Private Cloud (VPC) on AWS in a standard design

| Item                        | Description                                                                                                                                                                                                         |
| --------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Level**                   | Beginner                                                                                                                                                                                                            |
| **Duration**                | 30 minutes                                                                                                                                                                                                          |
| **AWS Services & Features** | IAM, Cloud9, CloudFormation, AWS CLI, AWS Console, VPC, Subnets, InternetGateway, Elastic IP, NAT Gateway, RouteTables, Network ACLs, Security Groups & EC2 Instances                                               |
| **AWS Region**              | US East 1 - N.Virginia                                                                                                                                                                                              |
| **Cost Estimate**           | If you are still in free-tier, this lab will cost \$0. However, if you are not on free-tier, you can expect to see a charge of approximately, **\$0.09 for 1 hour <validate this!></validate>** of running the lab. |

#### Preparation Material

If you are new to networking or to AWS, going through the following content that will bring you up to speed for the lab. If you already have a networking background, go through VPC Getting Started Video content in the links below

- **OSI and TCP/IP Model**
  - https://www.geeksforgeeks.org/layers-of-osi-model/
  - https://www.geeksforgeeks.org/tcp-ip-model/
- **What is IPv4?**
  - https://www.geeksforgeeks.org/introduction-and-ipv4-datagram-header/
  - https://www.geeksforgeeks.org/difference-between-private-and-public-ip-addresses/
- **What is IPv6?**
  - https://www.geeksforgeeks.org/internet-protocol-version-6-ipv6/
- **What is CIDR?**
  - https://www.keycdn.com/support/what-is-cidr
- **AWS VPC Getting Started** - Some great video content on Getting Started on AWS VPC over the years since 2016:
  - https://www.youtube.com/watch?v=Ul2NsPNh9Ik **Watch upto 29:00**
  - https://www.youtube.com/watch?v=jZAvKgqlrjY **Watch upto 24:40**
  - https://www.youtube.com/watch?v=hiKPPy584Mg **Watch upto 20:40**
- **How to do subnetting?**
  - https://www.cisco.com/c/en/us/support/docs/ip/routing-information-protocol-rip/13788-3.html
- **Online Subnet Builder Tool**
  - https://tidalmigrations.com/subnet-builder/

#### Architecture overview

Below is the architecture of the VPC that we will build in this lab.

![VPC](/Lab1_VPC_Arch.png)

#### Prerequisites and dependencies

You need an AWS account to start trying the labs. If you don't have an AWS account, you can create yourself one by following the steps as documented here: https://aws.amazon.com/premiumsupport/knowledge-center/create-and-activate-aws-account/

There are no other prerequisites or dependencies for this lab

#### Lab Contents

##### Step:1

Build a [VPC](https://docs.aws.amazon.com/vpc/latest/userguide/what-is-amazon-vpc.html) with an IPv4 address range. We will use a **CIDR of - 10.0.0.0/16** for the VPC. The VPC will be built in **[US East 1 AWS Region](https://aws.amazon.com/about-aws/global-infrastructure/regions_az/)** . The VPC will span 2 [Availability Zones (AZ)](https://aws.amazon.com/about-aws/global-infrastructure/regions_az/) - US East 1A and US East 1B.

##### Step:2

Deploy an [Internet Gateway (IGW)](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_Internet_Gateway.html) and attach it to the VPC created in step:1

##### Step:3

Deploy 2 public [subnets](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_Subnets.html) one per AZ. The public subnets will have CIDR ranges of **10.0.0.0/24 and 10.0.1.0/24** respectively.

Also deploy 2 private subnets one per AZ with CIDR of **10.0.2.0/24 and 10.0.3.0/24** respectively.

##### Step:4

Create two [ElasticIPs](https://docs.aws.amazon.com/AWSEC2/latest/WindowsGuide/elastic-ip-addresses-eip.html). Deploy 2 [NAT Gateways](https://docs.aws.amazon.com/vpc/latest/userguide/vpc-nat-gateway.html) one per public subnet and assign the ElasticIPs.

##### Step:5

Setup [Routetables](https://docs.aws.amazon.com/vpc/latest/userguide//WorkWithRouteTables.html). Build two routetables - one for public subnets and one for private subnets. Attach the routetables to the respective subnets

##### Step:6

Setup [NACL](https://docs.aws.amazon.com/vpc/latest/userguide/vpc-network-acls.html) and attach it to the private subnets

##### Step:7

Create two [Security Group(SG)](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_SecurityGroups.html) - one for ['bastion host'](https://en.wikipedia.org/wiki/Bastion_host) and one for 'secure host'

##### Step:8

Create two EC2 instances - one in one of the public subnets as the **'bastion host'** and one in one of the private subnets as the **'secure host'** . Attach the respective SG created in step:7 to the EC2 instances. From external world try to access the 'bastion host' over the instance's public IP address and test connectivity. From the 'bastion host' connect to the 'secure instance' via its private IP addresss. From the 'secure instance' try to test the outbound internet connectivity.

##### Step:9

Codify steps:1 through 9 as a [CloudFormation Template](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/Welcome.html) for reuse.

#### Cleanup

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
