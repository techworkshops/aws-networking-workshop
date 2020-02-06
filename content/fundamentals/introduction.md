---
title: "Introduction"
menuTitle: "Introduction"
date: 2019-12-20T10:22:08+05:30
weight: 1
---
#### What we will build

In this lab, we will create a network stack required to host a highly available 2-tier web application.

![VPC](/Lab1_VPC_Arch.png)

- Two Availability Zones for high availability and disaster recovery. Availability Zones are geographically distributed within a region and spaced for best insulation and stability in the event of a natural disaster. We recommend that you maximize your use of Availability Zones to isolate a data center outage.
- Separate subnets for unique routing requirements. We recommend using public subnets for external-facing resources and private subnets for internal resources. For each Availability Zone, we have one public subnet and one private subnet.
- Additional layer of security. We recommend using network access control lists (ACLs) as firewalls to control inbound and outbound traffic at the subnet level. In this example, we have a network ACL protected subnet in each Availability Zone. These network ACLs provide individual controls that you can customize as a second layer of defense.
- Independent routing tables configured for every private subnet to control the flow of traffic within and outside the VPC. The public subnets share a single routing table, because they all use the same internet gateway as the sole route to communicate with the internet.
- Highly available NAT gateways instead of NAT instances. NAT gateways offer major advantages in terms of deployment, availability, and maintenance.
- Spare capacity for additional subnets, to support your environment as it grows or changes over time.

#### Preparation Material

If you have familiarity with networking and AWS, here is a quick primer of the components that we will be referring in this lab:

- A **virtual private cloud (VPC)** is a virtual network dedicated to your AWS account. It spans all availability zones within a region.
- A **Subnet** is a range of IP addresses in your VPC. It spans one availability zone within a region. 
- A **Route Table** contains a set of rules, called routes, that are used to determine where network traffic is directed.
- An **Internet Gateway** is a horizontally scaled, redundant, and highly available VPC component that allows communication between instances in your VPC and the internet.
- A **NAT Gateway** is a managed NAT components that are used to let egress traffic from a private subnet.
- **Security Groups** are your first line of defense for your servers. It acts as a virtual firewall for your instance to control inbound and outbound traffic.

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