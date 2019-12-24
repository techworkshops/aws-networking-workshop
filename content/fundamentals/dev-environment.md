---
title: "Set up the Development Environment"
date: 2019-12-20T10:22:08+05:30
draft: true
weight : 2
---

After getting access to your AWS console, navigate to cloud9

```
https://console.aws.amazon.com/cloud9/home?region=us-east-1

```

1. Click on "Create Environment" and follow the wizard. 

2. Enter Name of the Environment to be: "AWS Network Workshop"

3. In the step "Configure Settings" leave the default configuration. 

4. You will see a summary as shown in the below screenshot

![Cloud 9 IDE Setup Summary](/cloud9-summary.PNG)

5. Click on "Create Environment"

6. If all goes well, you should now see an IDE as given below

![Cloud 9 Basic Tour](/cloud9_callouts_added.png)

7. Test if AWS cli works by issuing following command in the terminal
```
aws configure --profile default
```

If your profile is configured correctly, you will see an output as below

```
AWS Access Key ID [****************52FQ]: 
AWS Secret Access Key [****************xgyZ]:
Default region name [us-west-2]: 
Default output format [json]: 
```

