---
title: "Building the Network Stack"
date: 2019-12-20T10:22:08+05:30
draft: true
weight : 3
---

#### Step 1: Create VPC

```
aws ec2 create-vpc --cidr-block 10.0.0.0/16
```

In the output that's returned, take note of the VPC ID.

```
{
    "Vpc": {
        "VpcId": "vpc-2f09a348", 
        ...
    }
}

```
You can also add useful tags to the VPC created before 

```aws ec2 create-tags --resources vpc-2f09a348 --tags Key=Name,Value=sample-vpc```

#### Step 2: Create Subnets
Using the VPC ID from the previous step, create a subnet with a 10.0.1.0/24 CIDR block. This will be your DMZ subnet. 
```aws ec2 create-subnet --vpc-id vpc-2f09a348 --cidr-block 10.0.1.0/24 --availability-zone us-east-1a```
```aws ec2 create-tags --resources vpc-2f09a348 --tags Key=Name,Value=sample-vpc-sub-dmz```

Using the VPC ID from the previous step, create a subnet with a 10.0.2.0/24 CIDR block. This will be your private subnet. 

```aws ec2 create-subnet --vpc-id vpc-2f09a348 --cidr-block 10.0.2.0/24 --availability-zone us-east-1a```
```aws ec2 create-tags --resources vpc-2f09a348 --tags Key=Name,Value=sample-vpc-sub-priv```

#### Step 3: Configure DMZ Subnet
```
# Create Internet Gateway
aws ec2 create-internet-gateway
```

Take a note of the InternetGatewayId

```
{
    "InternetGateway": {
        ...
        "InternetGatewayId": "igw-1ff7a07b", 
        ...
    }
}
```
Take a note of the ID and attach it to the VPC created before

```
aws ec2 create-tags --resources igw-1ff7a07b --tags Key=Name,Value=sample-vpc-igw
aws ec2 attach-internet-gateway --vpc-id vpc-2f09a348 --internet-gateway-id igw-1ff7a07b
```

```

# Create Route table
aws ec2 create-route-table --vpc-id vpc-2f09a348
aws ec2 create-tags --resources rtb-35b6a651 --tags Key=Name,Value=sample-vpc-rtb-igw

# Attach it to DMZ Subnet
aws ec2 associate-route-table --subnet-id subnet-36d6191c --route-table-id rtb-35b6a651

```

#### Step 4: Configure Private Subnet


