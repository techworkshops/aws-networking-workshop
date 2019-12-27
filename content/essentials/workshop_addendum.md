---
title: "Deploy EC2 Instances"
menuTitle : "Deploy and Test Application"
date: 2019-12-20T10:22:08+05:30
draft: true
weight : 3
---

####  Deploy The Web Application
We will not cover in depth of hosting or running applications in this chapter. 
To understand the concept of security groups and NACL, we will instead deploy the following: 
1. EC2 instance that has a PHP webapp in public subnet. 
2. We will then configure security group to securely SSH into the machine and access via browser. 

Navigate to [Key Pairs](https://console.aws.amazon.com/ec2/home?region=us-east-1#KeyPairs:sort=keyName)
 1. Click on "_Create Key Pair_". 
 2. Provide the name as "network-workshop" and click "_Create_". 
 This will download a file called "_network-workshop.pem"_. We will use this pem file to SSH into the EC2 instances. 
 3. Navigate to [Intances](https://console.aws.amazon.com/ec2/home?region=us-east-1#Instances:sort=statusChecks)
 4. Click on "_Launch Instance_" button.
 5. Choose the second AMI that is titled as "Amazon Linux  AMI 2018.03.0"
 ![Choose Image](/chapter1/choose_ami.png?classes=border,shadow)
 6. In the next page, choose instance type as "t2.micro" and click on "Configure Instance Details" button
 7. In the page "Configure Instance Details", choose the VPC that we created earlier and _public_subnet_2_ and click on "_Add Storage_". 
 ![Choose Image](/chapter1/configure_instance.png?classes=border,shadow)
 8. Expand the Advanced Details section at the bottom of the page, and type the following initialization script information (you can use Shift-Enter to create the necessary line break, or alternatively you could type this into Notepad and copy & paste the results) into the User Data field (this will automatically install and start the Apache web server on launch) and click Next: Add Storage:
    
    TODO: The shell script needs to be fixed. 
    ```shell script 
    #include
    https://awstechbootcamp.s3.amazonaws.com/bootstrap.sh
    ```
 8. Leave the default details mentioned in "Add Storage" page and click on "Add Tags"
 9. Next, choose a "friendly name" for your instance. This name, more correctly known as a tag, will appear in the console once the instance launches. I named it "PHP Web Server"
 ![Choose Image](/chapter1/add_tags.png?classes=border,shadow)
 10. Move on to the next step "Configure Security Group". Provide a friendly name and click on "Add Rule" and select HTTP. Click on "Next: Launch Instance"  
 ![Choose Image](/chapter1/security_group.png?classes=border,shadow)
 11.  Select the keypair that we selected in step 2 and click on "I acknowledge" checkbox  and launch
 ![Choose Image](/chapter1/launch.png?classes=border,shadow)
 12.  Navigate to [Intances](https://console.aws.amazon.com/ec2/home?region=us-east-1#Instances:sort=statusChecks). You should now see the instance starting up. Wait for the instance to startup. Note down the public ip. 
 ![Choose Image](/chapter1/running_instance.png?classes=border,shadow)
 13.  In a separate tab navigate to http://<Your Instance's Public IP>. You should see a website as below
  ![Choose Image](/chapter1/running_website.png?classes=border,shadow)