---
title: "Set up IAM"
date: 2019-12-20T10:22:08+05:30
draft: true
weight : 1
---

You can create IAM identities (users, groups, roles) and assign custom permissions sets (IAM policies) to those identities. This allows you to grant each user access to only the services, resources, and information that they need to perform tasks. Each user can also be assigned unique security credentials, access keys, and multi-factor authentication devices.
Here is a quick tutorial on getting started with IAM

```
# list all user's info
aws iam list-users

# crate new user
aws iam create-user \
    --user-name aws-admin2

# create a group
aws iam create-group --group-name NetworkAdmin

# add a policy to a group - Policy by Job Function: https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_job-functions.html

aws iam attach-group-policy \
    --group-name NetworkAdmin \
    --policy-arn arn:aws:iam::aws:policy/NetworkAdministrator

# add a user to a group
aws iam add-user-to-group \
    --group-name NetworkAdmin \
    --user-name aws-admin2

```
