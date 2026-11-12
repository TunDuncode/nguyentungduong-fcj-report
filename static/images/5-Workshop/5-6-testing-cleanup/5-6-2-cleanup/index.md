---
title: "5.6.2. Review Costs and Preserve Evidence"
date: 2026-11-11T00:00:00+07:00
draft: false
weight: 2
---

# 5.6.2. Review Costs and Preserve Evidence

## Objective

Finish a lab session without avoidable charges while preserving the resources needed for the team's final demonstration.

## Cost checklist

1. Open **Billing → Cost Explorer / Bills** and record actual spending by service and Region.
2. Review **AWS Budgets** and recipient email addresses, especially around the 25%, 50%, and 100% thresholds of the group's USD 20/month plan.
3. Check **EC2 → Instances** and consider **Stop** when monitoring is not required. EBS and some attached resources can still incur costs.

![Three CloudWatch alarms after creation]({{< relURL "images/netmon-workshop/cloudwatch-alarms.webp" >}})

*Evidence: Three CloudWatch alarms after creation. Captured during the NetMon lab; the AWS account header has been removed.*

4. Review EBS volumes/snapshots, public IP allocations, NAT Gateways (if present), CloudWatch Logs retention, and disposable test resources.
5. Do not delete `NetworkDevices`, `NetworkAlerts`, `netmon-api`, `netmon-save-alert`, or the Cognito User Pool while the group still needs them for demonstrations or reporting.

## At final project closure

- Publish the report and sanitized evidence screenshots to the repository.
- Document resource dependencies: API Gateway → Lambda → DynamoDB; EventBridge → Lambda → DynamoDB; CloudWatch → SNS.
- Only after all teammates confirm that the system is no longer needed, delete resources in dependency order and review the following billing cycle.
- Do not assume stopping EC2 deletes every resource or eliminates all charges.

## Summary

The NetMon workshop covers VPC and EC2, CloudWatch monitoring, SNS notifications, EventBridge/Lambda/DynamoDB alert history, and a Cognito-protected HTTP API. Completion should be supported by actual end-to-end test evidence.

---

> **Publishing note:** Do not publish original images showing email addresses, login codes, or tokens. Screenshots in this pack come from the lab and have the account header removed; review them again before going public.

[← Back to chapter](../)
