---
title: "5.3. CloudWatch, SNS, and EventBridge"
date: 2026-11-11T00:00:00+07:00
draft: false
weight: 3
---

# 5.3. CloudWatch, SNS, and EventBridge

CloudWatch monitors CPU/RAM/Disk; SNS emails alerts, while EventBridge routes alarm state changes to Lambda and DynamoDB.

## Detailed practice lessons

- [5.3.1. Collect CPU, RAM, and Disk Metrics](5-3-1-metrics/)
- [5.3.2. Create CloudWatch Alarms and SNS Email](5-3-2-alarms-sns/)
- [5.3.3. Route Alarm Changes with EventBridge](5-3-3-eventbridge/)
- [5.3.4. Store Alert History with Lambda and DynamoDB](5-3-4-alert-history/)

![CloudWatch flow]({{< relURL "images/netmon-workshop/netmon-alert-flow.png" >}})
