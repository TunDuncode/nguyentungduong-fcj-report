---
title: "10. CloudWatch, SNS, EventBridge, and alert history"
date: 2026-10-31T09:00:00+07:00
weight: 10
draft: false
description: "CloudWatch, SNS, EventBridge, and alert history"
---

# 10. CloudWatch, SNS, EventBridge, and alert history

### Week 10 Objectives:

- Understand CloudWatch Alarm → SNS email and EventBridge → Lambda → DynamoDB.
- Collaborate with the monitoring workstream led by Mạnh Quân.
- Check stored alarm records and distinguish test events.

### Tasks to be carried out this week:

| Day | Task | Start Date | Completion Date | Reference Material |
| :--- | :--- | :--- | :--- | :--- |
| Saturday (on-site) | Review the three CPU, RAM, and disk alarms with 80%, 80%, and 85% test thresholds. | 31/10/2026 | 31/10/2026 | [CloudWatch alarms](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/CloudWatch_Alarms.html) |
| Sunday (independent study) | Inspect the netmon-alerts SNS topic, confirmed email subscription, and controlled test alerts. | 01/11/2026 | 01/11/2026 | [Amazon SNS](https://docs.aws.amazon.com/sns/latest/dg/welcome.html) |
| Monday (independent study) | Review netmon-alarm-state-rule receiving CloudWatch Alarm State Change events. | 02/11/2026 | 02/11/2026 | [CloudWatch events and EventBridge](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/cloudwatch-and-eventbridge.html) |
| Tuesday (independent study) | Check the netmon-save-alert Lambda and PutItem permission for recording alarms in NetworkAlerts. | 03/11/2026 | 03/11/2026 | [Amazon DynamoDB](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/Introduction.html) |

### Week 10 Achievements:

- Documented the team’s alert workflow across **CloudWatch, SNS, EventBridge, and DynamoDB**.
- The team confirmed SNS email delivery and resolved a `dynamodb:PutItem` access issue for alert recording.
- Recognized that CloudWatch thresholds alone do not prove simulated-device alerting is fully integrated.

