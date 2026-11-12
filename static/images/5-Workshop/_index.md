---
title: "5. Workshop"
date: 2026-11-11T00:00:00+07:00
draft: false
weight: 5
---

# 5. WORKSHOP — BUILDING NETMON ON AWS

## Overview

This workshop documents how to reproduce **An SME Network Infrastructure Management and Monitoring System on AWS with Serverless Services**. It follows the team's lab in **us-east-1**, presenting Console steps, checklists, and actual evidence screenshots in the same navigational format as the reference workshop.

**Data flow:** UI → Cognito → API Gateway → Lambda → DynamoDB; EC2 → CloudWatch → SNS / EventBridge → Lambda → DynamoDB.

![Management architecture]({{< relURL "images/netmon-workshop/netmon-api-flow.png" >}})

![Alert architecture]({{< relURL "images/netmon-workshop/netmon-alert-flow.png" >}})

## Hands-on chapters

1. [5.1. Environment Preparation & Region](5-1-preparation/)
   - [5.1.1. AWS Sign-in and Region](5-1-preparation/5-1-1-region-budget/)
   - [5.1.2. IAM Setup and Team Roles](5-1-preparation/5-1-2-iam/)
   - [5.1.3. AWS Budgets and Cost Controls](5-1-preparation/5-1-3-budget/)

2. [5.2. VPC and EC2 Infrastructure](5-2-infrastructure/)
   - [5.2.1. Create a VPC, Subnets, Routes, and IGW](5-2-infrastructure/5-2-1-vpc/)
   - [5.2.2. Launch an Ubuntu EC2 Instance](5-2-infrastructure/5-2-2-ec2/)
   - [5.2.3. Security Groups, IAM Roles, and Safe Access](5-2-infrastructure/5-2-3-security/)

3. [5.3. CloudWatch, SNS, and EventBridge](5-3-monitoring/)
   - [5.3.1. Collect CPU, RAM, and Disk Metrics](5-3-monitoring/5-3-1-metrics/)
   - [5.3.2. Create CloudWatch Alarms and SNS Email](5-3-monitoring/5-3-2-alarms-sns/)
   - [5.3.3. Route Alarm Changes with EventBridge](5-3-monitoring/5-3-3-eventbridge/)
   - [5.3.4. Store Alert History with Lambda and DynamoDB](5-3-monitoring/5-3-4-alert-history/)

4. [5.4. Lambda, DynamoDB, and API Gateway](5-4-serverless/)
   - [5.4.1. Create NetworkDevices and NetworkAlerts Tables](5-4-serverless/5-4-1-dynamodb/)
   - [5.4.2. Build the netmon-api Python Lambda](5-4-serverless/5-4-2-lambda-api/)
   - [5.4.3. Build an HTTP API with Eight Routes](5-4-serverless/5-4-3-api-gateway/)
   - [5.4.4. Test CRUD and Data Queries](5-4-serverless/5-4-4-crud-test/)

5. [5.5. Cognito, JWT, and the Test Interface](5-5-auth-frontend/)
   - [5.5.1. Create a Cognito User Pool and Web Client](5-5-auth-frontend/5-5-1-cognito/)
   - [5.5.2. Create a JWT Authorizer and OAuth Scopes](5-5-auth-frontend/5-5-2-jwt/)
   - [5.5.3. Build a VS Code Test Page](5-5-auth-frontend/5-5-3-test-ui/)
   - [5.5.4. Sign In with PKCE and Call Protected APIs](5-5-auth-frontend/5-5-4-frontend-login/)

6. [5.6. End-to-End Tests and Resource Cleanup](5-6-testing-cleanup/)
   - [5.6.1. Test from the UI to CloudWatch/DynamoDB](5-6-testing-cleanup/5-6-1-e2e/)
   - [5.6.2. Review Costs and Preserve Evidence](5-6-testing-cleanup/5-6-2-cleanup/)
   - [5.6.3. Clean Up CloudWatch, SNS, and EventBridge](5-6-testing-cleanup/5-6-3-monitoring-cleanup/)
   - [5.6.4. Clean Up Lambda, DynamoDB, and API Gateway](5-6-testing-cleanup/5-6-4-serverless-cleanup/)
   - [5.6.5. Clean Up Cognito and Networking Resources](5-6-testing-cleanup/5-6-5-auth-cleanup/)


## Observed progress and scope

- **Evidence available:** EC2, three CloudWatch alarms, SNS email, DynamoDB items, alert-storage Lambda, EventBridge rule, eight HTTP API routes, JWT Authorizer, CORS, and Lambda integration.
- **Still to verify:** final UI, the PKCE token exchange, and complete browser-to-DynamoDB CRUD.
- **Safety:** never publish addresses, passwords, AWS access keys, or tokens. Budget alerts do not cap spending.

> Screenshots are drawn from the user's own AWS lab captures; no GameHub Console images are represented as NetMon evidence.
