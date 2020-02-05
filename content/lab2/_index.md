+++
title = "Lab2: Elastic Load Balancing"
menuTitle="Lab2: Elastic Load Balancing"
weight = 1
chapter = true
+++

# Elastic Load Balancing

#### Overview

| Item                        | Description                                                                                                                                                                                                         |
| --------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Level**                   | Intermediate                                                                                                                                                                                                            |
| **Duration**                | 30 minutes                                                                                                                                                                                                          |
| **AWS Services & Features** | AWS Console, VPC, Subnets, InternetGateway, Elastic IP, NAT Gateway, RouteTables, Network ACLs, Security Groups & EC2 Instances                                               |
| **AWS Region**              | US East 1 - N.Virginia                                                                                                                                                                                              |
| **Cost Estimate**           | If you are still in free-tier, this lab will cost \$0. However, if you are not on free-tier, you can expect to see a charge of approximately, **\$0.09 for 1 hour** of running the lab. |

Elastic Load Balancing automatically distributes your incoming application traffic across multiple targets, such as EC2 instances. Elastic Load Balancing offers three types of load balancers that all feature the high availability, automatic scaling, and robust security necessary to make your applications fault tolerant. The three types of load balancers are: Application Load Balancers, Network Load Balancers, and Classic Load Balancers.

In this lab, we will deploy EC2 instances operating as web servers, and we'll configure Load Balancers to distribute between the instances. After everything is set up, we will simulate stress tests on the EC2 instances to test the horizontal scalablity.
