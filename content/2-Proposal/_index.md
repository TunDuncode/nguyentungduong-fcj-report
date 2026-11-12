---
title: "2.Proposal"
date: 2026-11-12
weight: 2
draft: false
---

# PROJECT PROPOSAL

**Project title:** Building a Network Infrastructure Management and Monitoring System for Small and Medium-Sized Enterprises on AWS with Serverless Services.

**Project format:** A three-member student team implementing a simulation-based AWS project, primarily in **US East (N. Virginia) – `us-east-1`**.

## 1. Executive Summary

This project aims to build a system that allows small and medium-sized enterprises (SMEs) to manage network-device records, monitor server resources, and detect abnormal conditions early. Rather than maintaining scattered spreadsheets or logging into each server to inspect its status, an administrator can view operational information in a central interface.

The team uses **Amazon VPC and EC2** to simulate the network infrastructure; **Amazon CloudWatch** to collect CPU, memory, and disk metrics; **Amazon SNS** for email notifications; **Amazon EventBridge and AWS Lambda** to capture events; and **Amazon DynamoDB** to store devices and alert history. Device management is exposed through **Amazon API Gateway, AWS Lambda, and Amazon Cognito**, providing HTTP APIs with authentication.

The solution combines an EC2 instance with serverless services; it is **not a 100% serverless system**. The main objective is a demonstrable learning environment in which the team can test and explain how an issue is detected, reported, recorded, and handled. It is a coursework prototype rather than a production enterprise product.

---

## 2. Problem Statement

### 2.1. Current Challenges

In many smaller organizations, device inventory and server monitoring are managed separately. Device information may be recorded in different files, CPU and memory usage may not be monitored continuously, and administrators may become aware of problems only after a service slows down or stops. Without alert history, determining whether an incident has already been addressed is also difficult.

Traditional monitoring deployments may require a dedicated management server, maintenance effort, and more complex setup. Given the time and cost limits of a student project, the team needs a model that is practical to deploy while still demonstrating core network-management procedures.

### 2.2. Proposed Solution

The system focuses on four functions:

1. **Device management:** create, view, update, delete, and search network-device records through an API backed by the `NetworkDevices` table.
2. **Resource monitoring:** use CloudWatch for CPU metrics and CloudWatch Agent or custom metrics for memory and disk utilization.
3. **Automatic alerting:** configure CloudWatch Alarms, send email through SNS, and route alarm-state changes through EventBridge to a Lambda function that stores events in `NetworkAlerts`.
4. **Administration interface:** authenticate with Cognito and display devices, metrics, alerts, and handling status on a dashboard.

### 2.3. Expected Benefits

The model reduces manual checks, centralizes information, and preserves a traceable alert history. The components are separated into testable services that can be extended later. AWS Budgets is used to monitor spending. The **USD 20 monthly budget is an alerting target, not a guaranteed spending cap or an automatic shutdown mechanism**.

---

## 3. Solution Architecture

The system has two main data flows: **device administration through HTTP APIs** and **monitoring, alerting, and alert-history storage**. AWS resources are configured and tested primarily in `us-east-1`.

### 3.1. System Architecture Diagram

{{< netmonarchitecture lang="en" >}}

*Figure 3.1. Proposed AWS architecture for the NetMon infrastructure management and monitoring system (a design diagram, not an AWS Console screenshot).*

### 3.2. AWS Services and Components

| Component | Role in the solution |
|---|---|
| **Amazon VPC** | Hosts `netmon-vpc` with CIDR `10.0.0.0/16`, separated into public and private subnets. |
| **Amazon EC2** | Runs the simulated `netmon-ec2-server` (Ubuntu 24.04 LTS, `t3.micro`). |
| **Security Groups and IAM** | Control network reachability and permissions for EC2 and Lambda. |
| **Amazon CloudWatch** | Collects CPU, memory, disk and log data and evaluates three alert thresholds. |
| **Amazon SNS** | Sends notifications to a confirmed email subscription. |
| **Amazon EventBridge** | Matches CloudWatch alarm-state changes and routes them to Lambda. |
| **AWS Lambda** | `netmon-api` implements APIs; `netmon-save-alert` records alert events in DynamoDB. |
| **Amazon API Gateway** | Provides HTTP endpoints for device inventory, alerts, and monitoring metrics. |
| **Amazon Cognito** | Manages users and provides JWTs checked by API Gateway. |
| **Amazon DynamoDB** | Stores inventory in `NetworkDevices` and alert history in `NetworkAlerts`. |
| **AWS Budgets** | Reports spending against a defined monthly budget. |

### 3.3. Data Flows

**Flow 1 — Device management:** A user signs in with Cognito → the browser calls API Gateway with a token → API Gateway validates the JWT → `netmon-api` reads or writes DynamoDB → the interface receives device or alert data.

**Flow 2 — Monitoring and alerting:** EC2 produces CPU, memory, and disk metrics → CloudWatch evaluates alarm thresholds → alarm-state changes can notify users through SNS and are matched by EventBridge → `netmon-save-alert` writes an event to `NetworkAlerts` → the alert-history page shows what happened and its handling status.

The VPC simulation includes **public subnet `10.0.0.0/20`**, **private subnet `10.0.128.0/20`**, dedicated route tables, and Internet Gateway `netmon-igw`. EC2 is in the public subnet. The private subnet demonstrates network segmentation; the design does not assume that a NAT Gateway or an EC2 instance is deployed there.

---

## 4. Technical Implementation

### 4.1. Implementation Phases

1. **Research and preparation:** study AWS services, select the deployment region, assign responsibilities, configure an AWS Budget, and draft the architecture.
2. **Infrastructure setup:** create a VPC, subnets, route tables, Internet Gateway, Security Group, IAM Role, and an Ubuntu EC2 instance for monitoring.
3. **Serverless API and database:** create the `NetworkDevices` and `NetworkAlerts` tables; implement Python Lambda functions with `boto3`; configure HTTP routes and Cognito authentication.
4. **Monitoring and integration:** configure CloudWatch metrics and alarms, SNS email, an EventBridge rule, an alert-recording Lambda function, the dashboard, and end-to-end tests.

### 4.2. API and Data Design

The main HTTP routes are:

| Method | Route | Purpose |
|---|---|---|
| GET | `/devices` | List devices. |
| POST | `/devices` | Add a device. |
| GET | `/devices/{id}` | View device details. |
| PUT | `/devices/{id}` | Update a device. |
| DELETE | `/devices/{id}` | Delete a device. |
| GET | `/alerts` | Retrieve alert history. |
| PUT | `/alerts/{id}` | Update alert-handling status. |
| GET | `/metrics` | Provide monitoring metrics to the dashboard. |

The `NetworkDevices` table stores fields such as `deviceId`, `deviceName`, `deviceType`, `ipAddress`, `status`, `instanceId`, and `region` where applicable. The `NetworkAlerts` table uses `eventId` to identify an event, with attributes including `alarmName`, `alarmState`, `alarmType`, `deviceId`, `eventTime`, and `handlingStatus`.

### 4.3. Technology Stack and Testing

- **Backend:** Python-based AWS Lambda functions with `boto3` for DynamoDB and CloudWatch integration.
- **Frontend:** an administration interface planned with HTML, CSS, and JavaScript, developed in Visual Studio Code and tested on localhost.
- **Authentication:** Cognito User Pool and an API Gateway JWT authorizer, with CORS configured for the test frontend origin.
- **Monitoring:** CloudWatch Alarms named `netmon-cpu-high-80`, `netmon-ram-high-80`, and `netmon-disk-high-85`.
- **Tests:** verify API responses, CRUD operations, alarm thresholds, SNS email, DynamoDB alert history, authorization, and UI behavior.

Actual AWS Console screenshots and test evidence are documented in **Section 5: Workshop**. Provisioning an AWS resource alone is not treated as proof that every intended feature has passed integration testing.

### 4.4. Team Responsibilities

| Team member | Main responsibilities |
|---|---|
| **Tùng Dương** | VPC, EC2, public/private subnets, routing, Internet Gateway, Security Groups, and infrastructure security. |
| **Xuân Đức** | Lambda, API Gateway, DynamoDB, device CRUD APIs, and data integration. |
| **Mạnh Quân** | CloudWatch, notifications, monitoring UI, and testing. |

---

## 5. Roadmap and Milestones

The planned duration is **12 weeks**, with one working session per week. Activities may be adjusted to match the team's actual progress.

| Week | Planned activity | Expected deliverable |
|---|---|---|
| **1** | Define the topic, scope, and relevant AWS services. | Requirements and role assignments. |
| **2** | Draft architecture, select the region, and set the budget. | Architecture diagram and AWS Budget. |
| **3** | Create VPC, subnets, Internet Gateway, and route tables. | Basic simulated network. |
| **4** | Configure Security Group, IAM Role, and Ubuntu EC2. | Running EC2 instance in the VPC. |
| **5** | Design DynamoDB tables. | `NetworkDevices` and `NetworkAlerts`. |
| **6** | Implement Lambda device listing and CRUD functions. | `netmon-api` and initial tests. |
| **7** | Configure API Gateway routes and CORS. | API callable from a test client. |
| **8** | Configure CloudWatch CPU, memory, and disk metrics/alarms. | Monitoring data and three alert thresholds. |
| **9** | Integrate SNS, EventBridge, and the alert-recording Lambda. | Email alerts and stored alarm events. |
| **10** | Configure Cognito, JWT authorization, and sign-in. | Basic authenticated access. |
| **11** | Improve the management UI and alert history; run integration tests. | Demonstration flows and issue tracking. |
| **12** | Collect screenshots, review cost, document the project, and report results. | Workshop, proposal, test evidence, and presentation. |

---

## 6. Budget Estimate and Cost Controls

The project uses AWS in `us-east-1` with a **USD 20 monthly cost budget** and notifications when actual costs exceed **25% (USD 5)**, **50% (USD 10)**, and **100% (USD 20)** of the budget. These values are **configured alert thresholds, not verified expenditure or a precise estimate**.

| Service | Potential cost drivers | Cost-control approach |
|---|---|---|
| **EC2 and EBS** | Instance runtime, storage, and related resources. | Stop EC2 outside test sessions and review remaining volumes. |
| **Public IPv4 address** | Usage may incur hourly charges. | Retain only when needed. |
| **CloudWatch** | Alarms, logs, custom metrics, and log retention. | Limit test data and set sensible retention. |
| **Lambda and API Gateway** | Requests and execution duration. | Avoid unbounded polling and excessive simulations. |
| **DynamoDB** | Reads, writes, and storage volume. | Keep the test dataset small. |
| **SNS, EventBridge, Cognito** | Messages, event volume, and service usage. | Monitor usage and avoid unnecessary traffic. |

**Cost principle:** compare AWS Billing/Cost Explorer with AWS Budgets throughout the project. Free Tier eligibility depends on the account and current service terms; services should not automatically be assumed free. **Budget alerts do not automatically stop EC2 or other AWS resources.**

---

## 7. Risk Assessment

### 7.1. Main Risks

| Risk | Impact | Mitigation |
|---|---|---|
| **Overly permissive Security Group rules** | High | Do not expose SSH (port 22) to the entire Internet unless strictly required; use least privilege. |
| **AWS credentials or account information exposed on GitHub** | High | Never commit access keys, secrets, or tokens; redact sensitive screenshot details before publication. |
| **JWT authentication or CORS errors** | Medium | Verify issuer, audience, scopes, callback URL, and frontend origin. |
| **Missing email alerts or event history** | Medium | Check SNS subscription confirmation, CloudWatch actions, EventBridge rules, Lambda permissions, and logs. |
| **Unexpected AWS charges** | Medium–high | Use AWS Budgets, review spending regularly, and stop or remove unused resources. |
| **Stale memory/disk metrics** | Medium | Check CloudWatch Agent or custom metrics, namespaces, dimensions, and IAM permissions. |

### 7.2. Contingency Plan

Keep source code in GitHub, assign IAM permissions by task, simulate devices when physical hardware is unavailable, and capture evidence after each test. If a service fails, begin with CloudWatch Logs and then test each step of the relevant event flow independently. If a real alarm transition is unavailable, use **clearly labeled test events** to verify the history-writing path; simulated incidents must not be presented as real operational failures.

---

## 8. Expected Outcomes

- **Device management:** REST-like APIs for creating, listing, updating, and deleting devices, backed by DynamoDB and accessible through the UI.
- **EC2 monitoring:** CPU, memory, disk, and server-status visibility through CloudWatch.
- **Detection and notification:** CPU and memory alarm thresholds at 80%, disk at 85%, and email notifications through SNS as configured.
- **Alert history:** EventBridge and Lambda store CloudWatch events in `NetworkAlerts`, including timestamps and handling status for follow-up.
- **Access security:** Cognito authentication, JWT-protected API routes, and appropriate IAM permissions.
- **Demonstration and reporting:** architecture documentation, AWS configuration screenshots, test scenarios, and a Workshop viewable through Hugo/GitHub Pages after publication.

The final evaluation should rely on **working test scenarios and evidence from AWS**, not only on a list of provisioned services. The prototype provides a foundation for future multi-server monitoring, but it is not yet a full-scale enterprise monitoring platform.
