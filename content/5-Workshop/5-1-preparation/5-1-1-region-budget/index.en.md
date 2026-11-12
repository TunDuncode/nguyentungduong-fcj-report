---
title: "5.1.1. AWS Sign-in and Region"
date: 2026-11-11T00:00:00+07:00
draft: false
weight: 1
---

# 5.1.1. AWS Sign-in and Region

## Objective

Select the correct `us-east-1` Region, verify AWS Console access, and create budget alerts for the lab.

## Steps

1. Sign in with an IAM user or a delegated account; **do not share the root account** across the team.
2. Select **United States (N. Virginia) — us-east-1** in the Region selector. Regional resources such as EC2, DynamoDB, Lambda, and API Gateway should be inspected in the same Region.

{{< netmonimg src="images/netmon-workshop/01-aws-region-us-east-1.png" alt="Select AWS region us-east-1" caption="Figure 01 – Select AWS region us-east-1" >}}


3. Navigate to **Billing and Cost Management → Budgets → Create budget**. Select a **Cost budget** and enter the planned limit (the group's earlier lab used **USD 20/month**).
4. Add alerts at **25%, 50%, and 100%**, if supported by your budget configuration, and verify the recipient email addresses.

5. Review **Cost Explorer** or **Bills** for actual expenses. Do not report the USD 20 budget as incurred charges.

## Verification

- The AWS Console displays `us-east-1` for project resources.
- The budget includes the intended email notifications.
- Capture the budget settings and Region while hiding sensitive information.

> **Cost note:** AWS Budgets sends notifications; it does not stop charges. EC2, EBS, CloudWatch, DynamoDB, SNS, and other services may still incur costs depending on usage.

---

> **Publishing note:** Do not publish original images showing email addresses, login codes, or tokens. Screenshots in this pack come from the lab and have the account header removed; review them again before going public.

[← Back to chapter](../)
