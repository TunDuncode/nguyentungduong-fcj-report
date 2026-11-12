---
title: "3. Technical Blogs"
weight: 3
chapter: true
draft: false
---

## Technical writing from my AWS NetMon internship project

During my internship (August 8 – November 14, 2026), I worked with my team on **NetMon**, an experimental network infrastructure management and monitoring solution for small and medium-sized businesses, using AWS Serverless services in the **us-east-1** Region.

The three articles below document the technologies I learned, the configuration and testing process, and lessons for future improvements. **These are personal technical drafts prepared for publication, not articles already published on AWS Study Group.**

| Article | Main topic | Link |
|---|---|---|
| **3.1** | Device CRUD using Lambda, HTTP API Gateway and DynamoDB | [Read Blog 1](./3.1-blog1/) |
| **3.2** | Monitoring and alerts with CloudWatch, SNS and EventBridge | [Read Blog 2](./3.2-blog2/) |
| **3.3** | Cognito sign-in, JWT authorization and dashboard integration | [Read Blog 3](./3.3-blog3/) |

### Project architecture at a glance

`Web UI → Amazon Cognito → API Gateway → AWS Lambda → DynamoDB`

`EC2 → Amazon CloudWatch Alarm → Amazon SNS (email)`

`CloudWatch alarm state change → EventBridge → Lambda → DynamoDB (alert history)`

> **Publication status:** Drafts hosted on the internship report site. Once an external blog is published, add its verified public URL here.
