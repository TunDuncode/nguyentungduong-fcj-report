---
title: "5.1.2. IAM Setup and Team Roles"
date: 2026-11-11T00:00:00+07:00
draft: false
weight: 2
---

# 5.1.2. IAM Setup and Team Roles

## Objective

Assign project responsibilities and configure IAM so that each teammate can work without sharing credentials.

## Team responsibilities

| Member | Responsibility |
|---|---|
| Tung Duong | VPC, public/private subnets, route tables, Internet Gateway, Security Groups, EC2 |
| Xuan Duc | Lambda, DynamoDB, API Gateway, device CRUD, and alert APIs |
| Manh Quan | CloudWatch, SNS, interface, and testing |

## Steps

1. Open **IAM → Users**. Create separate IAM users, or use AWS IAM Identity Center if it is available.
2. Enable **AWS Management Console access** only when needed; use strong passwords and MFA.
3. Create IAM groups or policies based on each member's tasks. Narrow broad AWS-managed policies after the initial lab.

4. For Lambda, inspect **Configuration → Permissions**. The `netmon-api` execution role needs appropriate access to `NetworkDevices`, `NetworkAlerts`, and CloudWatch metrics.

{{< netmonimg src="images/netmon-workshop/53-lambda-netmon-api-execution-role-permissions.png" alt="Lambda netmon-api execution role" caption="Figure 53 – Lambda netmon-api execution role" >}}


{{< netmonimg src="images/netmon-workshop/54-iam-netmon-api-role-permission-policies.png" alt="IAM role permission policies" caption="Figure 54 – IAM role permission policies" >}}


{{< netmonimg src="images/netmon-workshop/55-iam-netmon-api-access-policy-json.png" alt="JSON policy granting DynamoDB and CloudWatch actions" caption="Figure 55 – JSON policy granting DynamoDB and CloudWatch actions" >}}

5. The `netmon-save-alert` role should be limited to writing `NetworkAlerts` and CloudWatch Logs.

## Verification

Sign in as each user and validate granted operations. For `AccessDeniedException`, check the action and resource in CloudWatch Logs, then correct the specific permission rather than granting blanket `*` access.

> **Identity note:** AWS IAM users administer AWS resources; Cognito users sign in to NetMon. Deleting a Cognito user does not remove IAM or EC2 resources.

---

> **Publishing note:** Do not publish original images showing email addresses, login codes, or tokens. Screenshots in this pack come from the lab and have the account header removed; review them again before going public.

[← Back to chapter](../)
