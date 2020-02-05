+++
title = "Lab1: AWS Networking Fundamentals"
weight = 1
chapter = true
pre = ""
+++

# AWS Networking Essentials

#### Overview

| Item                        | Description                                                                                                                                                                                                         |
| --------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Level**                   | Beginner                                                                                                                                                                                                            |
| **Duration**                | 30 minutes                                                                                                                                                                                                          |
| **AWS Services & Features** | AWS Console, VPC, Subnets, InternetGateway, Elastic IP, NAT Gateway, RouteTables, Network ACLs, Security Groups & EC2 Instances                                               |
| **AWS Region**              | US East 1 - N.Virginia                                                                                                                                                                                              |
| **Cost Estimate**           | If you are still in free-tier, this lab will cost \$0. However, if you are not on free-tier, you can expect to see a charge of approximately, **\$0.09 for 1 hour** of running the lab. |

In this lab, we will create a network stack required to host a highly available 2-tier web application. 
We will create 2 public [subnets](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_Subnets.html) and 2 private subnets. One subnet per AZ to improve availability. We will then create an Internet Gateway and configure Route Teables to allow Public Subnet to be accesssible from Internet. We will create NAT Gateway to allow Private Subnets to access internet. Once done, we will validate the connectivity by deploying instances in private and public subnets.  
Below is the architecture that we will build in this lab.

![VPC](/Lab1_VPC_Arch.png)
