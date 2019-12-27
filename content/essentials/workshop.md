---
title: "AWS Networking Essentials Lab"
menuTitle : "Workshop"
date: 2019-12-20T10:22:08+05:30
draft: true
weight : 2
---

#### Step 1: Design
Lets try and build the network stack required for hosting a n-tier architecture. 
A n-tier architecture typically consists of 2 subnets - one public which can be accessed from the internet. 
And one private subnet where the application would be hosted. 
The subnets would be created in atleast 2 availability zones (AZs) to ensure high availability. 
At the end of the chapter we will build a stack as shown in below screenshot. 
![Network Setup](/chapter1/network_setup.png?classes=border,shadow)
#### Step 1: Create VPCs
Navigate to https://console.aws.amazon.com/vpc/home?region=us-east-1. 
Click on "_Your VPCs_" in the side bar and click on "_Create VPC_"
![Create VPC](/chapter1/create_vpc.png?classes=border,shadow)
Enter the name tag and CIDR block as mentioned in the screenshot and click on create. 
You should now see the created VPC as shown in the screenshot below
![Create VPC](/chapter1/created_vpc.png?classes=border,shadow)
#### Step 2: Create Subnets
Now that VPC is created, lets create subnets inside the VPC. 
Navigate to "_Subnets_" in the sidebar and click on "_Create Subnet_". 
In the screen that comes up, enter name, VPC that was created in Step 1, select the availabilty zone and the CIDR block.
 ![Create Subnet](/chapter1/create_subnet.png?classes=border,shadow)
The above screenshot shows the data for public_subnet_1. Please repeat the process for rest of the subnets

| Subnet Name | Availability Zone | CIDR |
| ------ | ----------- | ----------- |
| public_subnet_2   | us_east_1b | 10.0.1.0/24 |
| private_subnet_1 | us_east_1a | 10.0.2.0/24 |
| private_subnet_2    | us_east_1b | 10.0.3.0/24 |

If all goes well, you should now see the created subnets as shown below
 ![Created Subnets](/chapter1/created_subnets.png?classes=border,shadow)
#### Step 3: Create Internet Gateway and NAT Gateway
So far, we have only created VPC and the Subnets we have'nt yet made it to be accessible from the internet. 
For allowing communication between VPC and the internet we need to associate a component called ["Internet Gateway"](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_Internet_Gateway.html). 
Internet Gateway would be associated with the Public Subnets so that instances in the public subnet can be accessed from the internet. We will see how to associate with the public subnet in the next step.
Navigate to "_Internet Gateway_" in the sidebar and click on "_Create internet gateway_"
Provide the name tag and click create
![Create Internet Gateway](/chapter1/create_internet_gateway.png?classes=border,shadow)
Once created, select it and click on "_Actions > Attach to VPC_"
Select the VPC that we created in "_Step 1_"
![Attach to VPC](/chapter1/attach_to_vpc.png?classes=border,shadow)
Now the Internet Gateway is associated with the VPC. Lets now create a NAT Gateway.  Navigate to "_NAT Gateways_" in teh side bar and click on "_Create NAT Gateway_"
NAT Gateway should be located in the Public Subnet. 
Choose _public_subnet_2_ and click on "_Create New EIP_" and click on "Create a NAT Gateway".
![Create NAT Gateway](/chapter1/create_nat_gateway.png?classes=border,shadow)
Ok so far, we have created the Internet Gateway and NAT Gateway lets see how to associate the same with the subnet in the next step. 
#### Step 4: Configure the Route Tables
Click on "_Route Tables_" in the side bar and filter by the VPC. You would see a route table that already exists. This is the Main Route Table. It controls the routing for all subnets that are not explicitly associated with any other route table.
We will use the "Main Route Table" for routing traffic from Internet to Public Subnet. 
We will create a custom route table for routing traffic from private subnet to internet via NAT Gateway. 
Click on the Main Route Table, navigate to "_Routes_" and click on "_Edit Routes_". For all traffic to the internet destination (0.0.0.0/0), the target should be the internet gateway that we created in the previous step as shown below.
Click on "_Save Route_" 
![Configure Route](/chapter1/route_to_igw.png?classes=border,shadow)
Now this step makes all the subnets public. This is because since there is no explicit subnet associations all subnet will be associated to the main route table which allows traffic to and from internet. 

So, to avoid this lets create a custom route table and associate with the private subnets. 
Click on "_create route table_" and provide details as shown in below screenshot. 
![Create Custom Route](/chapter1/create_private_route_table.png?classes=border,shadow)
Now, click on the newly created route table, click on "_Routes_" and "_Edit Routes_". Make a new entry to divert and traffic to internet (0.0.0.0/0) to NAT Gateway. 
Now Navigate to "_Subnet Associations_" and click on "_Edit subnet associations_". 
Select private_subnet_1 and private_subnet_2 to the route table as shown in the below screenshot and click "Save".
![Create Subnet Associations](/chapter1/edit_subnet_private_associations.png?classes=border,shadow)
 
Now the public subnets are associated with Internet Gateway and Private Subnets are associated with the NAT gateway via the Route Tables. 
![Created Routes](/chapter1/created_route_tables.png?classes=border,shadow)

Congratulations ! You have created a network stack for a n-tier application from scratch. 
In the next chapter, lets put this stack to use by deploying a web-application. 
