---
title: "5.6.1. Test from the UI to CloudWatch/DynamoDB"
date: 2026-11-11T00:00:00+07:00
draft: false
weight: 1
---

# 5.6.1. Test from the UI to CloudWatch/DynamoDB

## Objective

Run reproducible tests showing that the team's infrastructure, backend, and monitoring/interface components work together as one workflow.

![Testing CloudWatch from CloudShell]({{< relURL "images/netmon-workshop/cloudshell-test.webp" >}})

*Evidence: Testing CloudWatch from CloudShell. Captured during the NetMon lab; the AWS account header has been removed.*


![NetworkAlerts stores event history]({{< relURL "images/netmon-workshop/dynamodb-alerts-two.webp" >}})

*Evidence: NetworkAlerts stores event history. Captured during the NetMon lab; the AWS account header has been removed.*


![Eight API routes connected to netmon-api]({{< relURL "images/netmon-workshop/api-gateway-integration.webp" >}})

*Evidence: Eight API routes connected to netmon-api. Captured during the NetMon lab; the AWS account header has been removed.*


## Suggested test cases

| ID | Test action | Expected result |
|---|---|---|
| T01 | Request GET `/devices` without JWT | `401 Unauthorized` |
| T02 | Sign in with Cognito and PKCE | Obtain a valid Access Token |
| T03 | GET `/devices` with `read` scope | Receive the device list |
| T04 | POST `/devices` with `TEST-SW01` | Record created in `NetworkDevices` |
| T05 | GET/PUT `/devices/{id}` | Read and update the test device |
| T06 | DELETE `/devices/{id}` | Delete only the test device |
| T07 | GET `/alerts` | Read events in `NetworkAlerts` |
| T08 | PUT `/alerts/{id}` | Change `handlingStatus` to `Acknowledged` or `Resolved` |
| T09 | GET `/metrics` | Get real CloudWatch CPU data when available |
| T10 | Change a demo alarm state in a controlled test | Verify SNS and stored alert history |

## Evidence

Capture Cognito Users (hide email addresses for public use), JWT routes, Lambda Test, DynamoDB Scan, CloudWatch Alarms, EventBridge rule, redacted SNS email, and API Test results. Label evidence screenshots `T01`, `T02`, etc.

## Reporting

Mark a case **Pass** only after executing it and collecting evidence. Mark untested cases as `Pending`, rather than assuming success. Never delete actual EC2 records; operate on `TEST-` device IDs only.

---

> **Publishing note:** Do not publish original images showing email addresses, login codes, or tokens. Screenshots in this pack come from the lab and have the account header removed; review them again before going public.

[← Back to chapter](../)
