---
title: "5.6.4. Clean Up Lambda, DynamoDB, and API Gateway"
date: 2026-11-11T00:00:00+07:00
draft: false
weight: 4
---

# 5.6.4. Clean Up Lambda, DynamoDB, and API Gateway

## Before removing resources

Finish the demo and back up relevant screenshots, logs, API configuration, and test data. **Deleting a DynamoDB table may irreversibly remove data**.

## Steps

1. **DynamoDB:** Export or back up `NetworkDevices` and `NetworkAlerts` before deletion. Do not remove them while the frontend is still being tested.
2. **API Gateway:** Document the eight Routes, Authorizer, CORS, Stage, and Integration for `netmon-management-api`, then delete it only when no frontend depends on it.

![DynamoDB project table list]({{< relURL "images/netmon-workshop/dynamodb-tables.webp" >}})

*Evidence: DynamoDB project table list. Captured during the NetMon lab; the AWS account header has been removed.*

3. **AWS Lambda:** Review event targets and triggers before deleting `netmon-api` or `netmon-save-alert`.
4. **IAM roles:** Remove only roles dedicated to services that have been retired; preserve any role shared with EC2 or other applications.

![Eight API routes connected to netmon-api]({{< relURL "images/netmon-workshop/api-gateway-integration.webp" >}})

*Evidence: Eight API routes connected to netmon-api. Captured during the NetMon lab; the AWS account header has been removed.*

5. **CloudWatch logs:** Log groups may remain after Lambda deletion, so check them separately.

## Verification

Confirm resource identities in `us-east-1` before deleting anything; do not affect other team members' projects.

---

> **Publishing note:** Do not publish original images showing email addresses, login codes, or tokens. Screenshots in this pack come from the lab and have the account header removed; review them again before going public.

[← Back to chapter](../)
