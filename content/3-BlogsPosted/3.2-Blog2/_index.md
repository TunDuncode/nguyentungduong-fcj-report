---
title: "3.2. Monitoring EC2 and Recording Alerts on AWS"
date: 2026-11-12T00:00:00+07:00
weight: 2
chapter: false
draft: false
---

## 1. Why our monitoring project needs alert history

A device inventory alone does not tell an administrator whether a server is healthy. In our NetMon internship project, the team explored **Amazon CloudWatch, SNS, EventBridge, Lambda and DynamoDB** to collect metrics, send notifications and keep a record of alarm events.

Our hands-on infrastructure includes the Ubuntu 24.04 EC2 instance **`netmon-ec2-server`**, together with additional simulated network-device records. My responsibility was primarily the Serverless backend; I collaborated with the monitoring and UI workstreams to understand how alert data reaches the application.

## 2. Two connected workflows

**Notification path:**

`EC2 → CloudWatch metrics → CloudWatch Alarm → Amazon SNS → Email`

**Alert-history path:**

`Alarm state change → EventBridge → Lambda netmon-save-alert → DynamoDB NetworkAlerts`

SNS helps notify an administrator promptly. The DynamoDB history makes it possible to display when alerts happened and whether they have been handled.

## 3. Metrics and alarm states

The main monitoring topics were:

- **CPU utilization** of the EC2 instance.
- **Memory utilization** of the operating system.
- **Disk utilization** to spot storage pressure.
- **Alarm states** such as `OK`, `ALARM` and `INSUFFICIENT_DATA`.

A technical distinction matters: EC2 publishes `CPUUtilization` as a standard CloudWatch metric, whereas **OS memory and filesystem metrics usually require the CloudWatch Agent or custom metrics**. They should not be described as built-in EC2 metrics without that setup.

## 4. Alarm configuration and testing

For every CloudWatch Alarm, we need to verify the metric and dimensions, threshold, evaluation periods and intended SNS action. A test threshold used during the internship should be documented as an **educational setting**, not recommended blindly for production systems.

We also learned to distinguish CloudWatch operational alarms from **AWS Budgets cost notifications**. Both send alerts, but they monitor different conditions.

## 5. Using DynamoDB for alert history

Our alert history is stored in **`NetworkAlerts`**. A useful record can include the source Alarm name, the related device or instance, timestamp, severity and handling status. In the UI, I wanted two clearly visible states: **New** and **Resolved**, making the history useful after the original email notification.

A more robust implementation should consider duplicate EventBridge events, consistent timestamps, event identifiers and safe status updates when two administrators act on the same alert.

## 6. Lessons learned

The key lesson is that monitoring is a workflow, not simply a CPU chart:

`Metric → detection threshold → notification → stored history → administrator action`

Combining real EC2 monitoring with simulated device records makes it easier to demonstrate the system while identifying where actual AWS telemetry ends and test data begins.

**Potential improvements:** filtering by date and status, consistent event schemas, duplicate-event handling and cost tracking through AWS Billing and Budgets.

## 7. References

- [Amazon CloudWatch](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/WhatIsCloudWatch.html)
- [CloudWatch Agent metrics](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/metrics-collected-by-CloudWatch-agent.html)
- [Amazon EventBridge](https://docs.aws.amazon.com/eventbridge/latest/userguide/eb-what-is.html)
- [Amazon SNS](https://docs.aws.amazon.com/sns/latest/dg/welcome.html)

*Publication status: personal draft, not yet published on AWS Study Group.*
