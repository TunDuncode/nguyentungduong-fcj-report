---
title: "5.1.3. AWS Budgets and Cost Controls"
date: 2026-11-11T00:00:00+07:00
draft: false
weight: 3
---

# 5.1.3. AWS Budgets and Cost Controls

## Goal

Set up AWS cost monitoring for the lab. **A USD 20 budget is an alert threshold—not actual spending or a hard spending cap**.

## Console steps

1. Open **Billing and Cost Management → Budgets → Create budget**; choose **Cost budget**.
2. Choose **Monthly**, enter **USD 20**, and name the budget `netmon-monthly-budget` or another meaningful name.
3. Configure percentage-based email alerts. During the lab, the team adjusted one alert threshold to **25%**; other useful thresholds are 50% and 100%.
4. Enter the alert recipient email and complete any email verification required.
5. Review actual charges under **Cost Explorer** or **Bills**, particularly EC2, EBS, CloudWatch, DynamoDB, and any networking resources.

## Verification

- Confirm that the budget is listed and recipients are correct.
- Check the currency, monthly period, and warning thresholds.
- Redact email addresses before publishing cost-console screenshots.

> Note: EC2 uptime, EBS storage, public IPv4, NAT Gateway (if used), and CloudWatch usage may incur charges. Do not assume the entire system is free.



![Illustrative workflow diagram]({{< relURL "images/netmon-workshop/netmon-cost-flow.png" >}})

---

> **Publishing note:** Do not publish original images showing email addresses, login codes, or tokens. Screenshots in this pack come from the lab and have the account header removed; review them again before going public.

[← Back to chapter](../)
