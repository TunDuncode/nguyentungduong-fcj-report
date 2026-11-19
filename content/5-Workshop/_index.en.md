---
title: "5. Workshop"
date: 2026-11-11T00:00:00+07:00
draft: false
weight: 5
---

# 5. WORKSHOP — BUILDING NETMON ON AWS

## Overview

NetMon is an SME network infrastructure management and monitoring system on AWS, combining EC2 infrastructure with serverless services. This workshop follows the team's implementation in `us-east-1`, from account preparation, networking, and metric collection to API design, authentication, interface operation, and testing.

## Architecture and system operation

| Component | Role |
|---|---|
| VPC, Subnet, Security Group, EC2 | Network infrastructure and the monitored Ubuntu server |
| CloudWatch and CloudWatch Agent | Collect EC2 CPU, memory, disk, and traffic metrics |
| SNS | Send alert notifications by email |
| EventBridge and Lambda | Route alarm state changes and store event history |
| DynamoDB | Store devices and alert events |
| API Gateway and Lambda | Provide management, metric retrieval, and alert handling APIs |
| Cognito | Authenticate users and issue access tokens |
| HTML, CSS, JavaScript | Provide the NetMon interface and display data |

**Management flow:** The browser authenticates with Cognito, then sends its JWT to API Gateway → Lambda → DynamoDB. Lambda also reads CloudWatch when retrieving EC2 metrics.

**EC2 monitoring flow:** EC2/CloudWatch Agent → CloudWatch → Alarm. The alarm sends notifications to SNS; state-change events are separately routed by EventBridge to Lambda for persistence in DynamoDB.

**Simulation flow:** Routers, switches, and devices without live collectors are represented by simulated data. CPU, memory, and status change according to simulation logic; automatic alert generation and SNS delivery depend on the deployed monitor and trigger schedule. Simulated values are not physical-device measurements.

## Workshop outcomes

- Manage, search, and inspect devices using CRUD.
- Monitor CPU, memory, and EC2 traffic while distinguishing live and simulated sources.
- Inspect and handle alerts, review logs, and check AWS connectivity.
- Protect APIs with JWT, restrict permissions, and control costs.

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
   - [5.4.5. Device Simulation and Automated Monitoring](5-4-serverless/5-4-5-simulation/)

5. [5.5. Cognito, JWT, and the NetMon Interface](5-5-auth-frontend/)
   - [5.5.1. Create a Cognito User Pool and Web Client](5-5-auth-frontend/5-5-1-cognito/)
   - [5.5.2. Create a JWT Authorizer and OAuth Scopes](5-5-auth-frontend/5-5-2-jwt/)
   - [5.5.3. Build a VS Code Test Page](5-5-auth-frontend/5-5-3-test-ui/)
   - [5.5.4. Sign In with PKCE and Call Protected APIs](5-5-auth-frontend/5-5-4-frontend-login/)
   - [5.5.5. Operate the NetMon Management Interface](5-5-auth-frontend/5-5-5-netmon-interface/)

6. [5.6. End-to-End Tests and Resource Cleanup](5-6-testing-cleanup/)
   - [5.6.1. Test from the UI to CloudWatch/DynamoDB](5-6-testing-cleanup/5-6-1-e2e/)
   - [5.6.2. Review Costs and Preserve Evidence](5-6-testing-cleanup/5-6-2-cleanup/)
   - [5.6.3. Clean Up CloudWatch, SNS, and EventBridge](5-6-testing-cleanup/5-6-3-monitoring-cleanup/)
   - [5.6.4. Clean Up Lambda, DynamoDB, and API Gateway](5-6-testing-cleanup/5-6-4-serverless-cleanup/)
   - [5.6.5. Clean Up Cognito and Networking Resources](5-6-testing-cleanup/5-6-5-auth-cleanup/)

## Results and verification scope

The lab recorded VPC/EC2 configuration, three alarms, test SNS email delivery, EventBridge, DynamoDB data, the HTTP API, and the JWT authorizer. Lambda returned HTTP 200 in a device-list test and retrieved EC2 CPU, memory, NetworkIn, and NetworkOut. The local demo interface was tested for CRUD, simulated data, and alert handling.

For a live AWS demonstration, revalidate browser sign-in, CRUD, handling-status persistence, and automatic email delivery. Configuration screenshots or a local demo do not establish these outcomes. Network topology is illustrative; automatic physical router/switch discovery through SNMP has not been established.

Evidence screenshots reflect different implementation stages. Keep resources required for the project presentation until the demonstration is complete. Never publish credentials or tokens.
