---
title: "Lab"
menuTitle : "Lab"
date: 2019-12-20T10:22:08+05:30
weight : 2
---

#### Step 1: Create VPCs

Navigate to [console](https://console.aws.amazon.com/vpc/home?region=us-east-1).
Click on "_Your VPCs_" in the left hand menu  and click on "_Create VPC_".
![Create VPC](/chapter1/create_vpc.png?classes=border,shadow)
Enter the name tag as **_workshop-vpc_** and CIDR block as **10.0.0.0/16** and click on "_Create_".
You should now see the created VPC as shown in the screenshot below
![Create VPC](/chapter1/created_vpc.png?classes=border,shadow)

#### Step 2: Create Subnets

Navigate to "_Subnets_" in the left hand menu and click on "_Create Subnet_".
In the screen that comes up, enter name, VPC that was created in Step 1, select the availabilty zone and the CIDR block as given in the screenshot.
 ![Create Subnet](/chapter1/create_subnet.png?classes=border,shadow)
Repeat the process for other VPCs. The below table gives details of how each subnet is configured.  

| Subnet Name | Availability Zone | CIDR |
| ------ | ----------- | ----------- |
| public_subnet_1   | us_east_1a | 10.0.0.0/24 |
| public_subnet_2   | us_east_1b | 10.0.1.0/24 |
| private_subnet_1 | us_east_1a | 10.0.2.0/24 |
| private_subnet_2    | us_east_1b | 10.0.3.0/24 |

At the end of this step,  you should now see all the created subnets as shown below
 ![Created Subnets](/chapter1/created_subnets.png?classes=border,shadow)

#### Step 3: Create Internet Gateway and NAT Gateway

Navigate to "_Internet Gateway_" in the sidebar and click on "_Create internet gateway_"
Provide the name tag **igw_workshop_vpc** and click create
![Create Internet Gateway](/chapter1/create_internet_gateway.png?classes=border,shadow)
Once created, select it and click on "_Actions > Attach to VPC_"
Select the VPC that was created in "_Step 1_"
![Attach to VPC](/chapter1/attach_to_vpc.png?classes=border,shadow)
Now the Internet Gateway is associated with the VPC. Lets now create a NAT Gateway. Navigate to "_NAT Gateways_" in the side bar and click on "_Create NAT Gateway_"
Choose _public_subnet_1_ and click on "_Create New EIP_" and click on "Create a NAT Gateway".
![Create NAT Gateway](/chapter1/create_nat_gateway.png?classes=border,shadow)
Repeat the step for _public_subnet_2_

{{% notice tip %}}
Ensure that NAT gateways are associated to an Availabilty Zone. In production, we need to ensure they are deployed in at least two Availability Zones (AZs) in order to ensure high-availability of Egress internet traffic.
{{% /notice %}}

#### Step 4: Configure the Route Tables

Click on "_Route Tables_" in the left-hand menu and filter by the VPC. You would see a route table that already exists. This is called the Main Route Table. It controls the routing for all subnets that are not explicitly associated with any other route table. We will use the "Main Route Table" for routing traffic from Internet to Public Subnet.

We will then create a custom route table for routing traffic from private subnet to internet via NAT Gateway.
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

Congratulations ! You have created a network stack for a n-tier application from scratch. We will now test the connectivity by deploying EC2 instances.

#### Deploy EC2 instance in the Public Subnet

Navigate to [Key Pairs](https://console.aws.amazon.com/ec2/home?region=us-east-1#KeyPairs:sort=keyName)
 1. Click on "_Create Key Pair_".
 2. Provide the name as "network-workshop" and click "_Create_".
 This will download a file called "_network-workshop.pem"_. We will use this pem file to SSH into the EC2 instances.
 3. Navigate to [Intances](https://console.aws.amazon.com/ec2/home?region=us-east-1#Instances:sort=statusChecks)
 4. Click on "_Launch Instance_" button.
 5. Choose the AMI that is titled as "Amazon Linux  AMI 2018.03.0"
 ![Choose Image](/chapter1/choose_ami.png?classes=border,shadow)
 6. In the next page, choose instance type as "t2.micro" and click on "Configure Instance Details" button
 7. In the page "Configure Instance Details", choose the VPC that we created earlier and _public_subnet_2_ and click on "_Add Storage_".
 ![Choose Image](/chapter1/configure_instance.png?classes=border,shadow)
 8. Leave the default details mentioned in "Add Storage" page and click on "Add Tags"
 9. Next, choose a "friendly name" for your instance. This name, more correctly known as a tag, will appear in the console once the instance launches. I named it "Web Server"
 ![Choose Image](/chapter1/add_tags.png?classes=border,shadow)
 10. Move on to the next step "Configure Security Group". Provide a friendly name and click on "Add Rule" and select SSH. Click on "Next: Launch Instance"  
 ![Choose Image](/chapter1/security_group.png?classes=border,shadow)
 11. Select the keypair that we selected in step 2 and click on "I acknowledge" checkbox  and launch
 ![Choose Image](/chapter1/launch.png?classes=border,shadow)
 12. Navigate to [Intances](https://console.aws.amazon.com/ec2/home?region=us-east-1#Instances:sort=statusChecks). You should now see the instance starting up. Wait for the instance to startup. Note down the public ip.
 ![Choose Image](/chapter1/running_instance.png?classes=border,shadow)
 13. Once the instance has started up, click the Connect button up top. There will be a window popping up with an example SSH command. This will get us in, but remember to take the location of the .pem file into account when you run it. In a terminal, run these:
 ```
 ssh -i /path_to/network-workshop.pem ec2-user@your_public_ip
 ```
 We'll answer yes to the prompt asking if we're sure we want to connect, and should land at a command prompt in our bastion host.

 TODO: Add steps for EC2 in Private Subnet and how to test connectivity between bastion host and private subnet.