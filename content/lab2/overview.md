---
title: "Overview"
menuTitle: "Overview"
date: 2019-12-20T10:22:08+05:30
weight: 1
---

| Item                        | Description                                                                                                                                                                                                         |
| --------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Level**                   | Beginner                                                                                                                                                                                                            |
| **Duration**                | 30 minutes                                                                                                                                                                                                          |
| **AWS Services & Features** | AWS Console, VPC, Subnets, InternetGateway, Elastic IP, NAT Gateway, RouteTables, Network ACLs, Security Groups & EC2 Instances                                               |
| **AWS Region**              | US East 1 - N.Virginia                                                                                                                                                                                              |
| **Cost Estimate**           | If you are still in free-tier, this lab will cost \$0. However, if you are not on free-tier, you can expect to see a charge of approximately, **\$0.09 for 1 hour** of running the lab. |

#### Overview

In this lab, we will create a network stack required to host a highly available 2-tier web application. 
We will create 2 public [subnets](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_Subnets.html) and 2 private subnets. One subnet per AZ to improve availability. We will then create an Internet Gateway and configure Route Teables to allow Public Subnet to be accesssible from Internet. We will create NAT Gateway to allow Private Subnets to access internet. Once done, we will validate the connectivity by deploying instances in private and public subnets.  
Below is the architecture that we will build in this lab.

![VPC](/Lab1_VPC_Arch.png)

#### Preparation Material

If you are familiar with networking and AWS, here is a quick primer of the components that we will be using in this lab:

- A virtual private cloud (VPC) is a virtual network dedicated to your AWS account. It spans all availability zones within a region.
- A subnet is a range of IP addresses in your VPC. It spans one availability zone within a region. 
- A route table contains a set of rules, called routes, that are used to determine where network traffic is directed.
- An internet gateway is a horizontally scaled, redundant, and highly available VPC component that allows communication between instances in your VPC and the internet.
- A NAT Gateway is a managed NAT components that are used to let egress traffic from a private subnet.
- Security groups are your first line of defense for your servers. It acts as a virtual firewall for your instance to control inbound and outbound traffic.

If you are totally new to networking or to AWS, going through the following content will help you bring  up to speed for the lab.

- **OSI and TCP/IP Model**
  - [OSI Layers](https://www.geeksforgeeks.org/layers-of-osi-model/)
  - [TCP / IP Basics](https://www.geeksforgeeks.org/tcp-ip-model/)
- **What is IPv4?**
  - [IP V4](https://www.geeksforgeeks.org/introduction-and-ipv4-datagram-header/)
  - [Public and Private IPs](https://www.geeksforgeeks.org/difference-between-private-and-public-ip-addresses/)
- **What is IPv6?**
  - [IP V6](https://www.geeksforgeeks.org/internet-protocol-version-6-ipv6/)
- **What is CIDR?**
  - [CIDR](https://www.keycdn.com/support/what-is-cidr)
- **AWS VPC Getting Started** - Some great video content on Getting Started on AWS VPC over the years since 2016:
  - [VPC Fundamentals](https://www.youtube.com/watch?v=Ul2NsPNh9Ik) **Watch upto 29:00**
  - [VPC Fundamentals](https://www.youtube.com/watch?v=jZAvKgqlrjY) **Watch upto 24:40**
  - [AWS Networking  Fundamentals](https://www.youtube.com/watch?v=hiKPPy584Mg) **Watch upto 20:40**
- **How to do subnetting?**
  - [Subnetting](https://www.cisco.com/c/en/us/support/docs/ip/routing-information-protocol-rip/13788-3.html)
- **Online Subnet Builder Tool**
  - [Subnet Builder](https://tidalmigrations.com/subnet-builder/)

#### Prerequisites and dependencies

The only pre-requisite for this lab is to have an AWS account. If you don't have an AWS account, you can create yourself one by following the steps as documented here: [Create AWS Account](https://aws.amazon.com/premiumsupport/knowledge-center/create-and-activate-aws-account/)

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