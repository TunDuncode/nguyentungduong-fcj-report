---
title: "5.6.5. Clean Up Cognito and Networking Resources"
date: 2026-11-11T00:00:00+07:00
draft: false
weight: 5
---

# 5.6.5. Clean Up Cognito and Networking Resources

## Goal

Revoke access after the project and remove infrastructure that may continue generating charges.

## Cleanup steps

1. **Amazon Cognito:** Confirm the User Pool used by `netmon-web-client`. An application user in Cognito is different from an IAM user who accesses AWS Console.
2. When testing is complete, back up relevant configuration and remove the App Client, Resource Server, and User Pool as appropriate. Deleting the pool prevents NetMon users from signing in.

![Cognito User Pool and App Client creation success]({{< relURL "images/netmon-workshop/cognito-success.webp" >}})

*Evidence: Cognito User Pool and App Client creation success. Captured during the NetMon lab; the AWS account header has been removed.*

3. **EC2:** For a temporary pause, **Stop the instance**. Stopping does **not** automatically delete EBS volumes or all public IPv4-related costs.
4. When ending the lab, inspect `netmon-ec2-server`, EBS, Elastic IP/Public IPv4, VPC, Internet Gateway, route tables, NAT Gateway (if any), Security Groups, and IAM instance profile before cleanup.

![EC2 instance shown in the Instances list]({{< relURL "images/netmon-workshop/ec2-list.webp" >}})

*Evidence: EC2 instance shown in the Instances list. Captured during the NetMon lab; the AWS account header has been removed.*

5. **Billing:** Recheck Bills and Cost Explorer in the following days because charge reporting can lag.

## Warning

Do not delete the AWS root account, the default VPC, or shared resources just to tidy up the console.

---

> **Publishing note:** Do not publish original images showing email addresses, login codes, or tokens. Screenshots in this pack come from the lab and have the account header removed; review them again before going public.

[← Back to chapter](../)
