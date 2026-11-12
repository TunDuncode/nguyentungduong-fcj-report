---
title: "5. DynamoDB design for devices and alert history"
date: 2026-09-19T09:00:00+07:00
weight: 5
draft: false
description: "DynamoDB design for devices and alert history"
---

# 5. DynamoDB design for devices and alert history

### Week 5 Objectives:

- Choose partition keys and attributes for device records.
- Prepare the alert-history structure used by the dashboard.
- Learn item operations through the AWS Console and boto3.

### Tasks to be carried out this week:

| Day | Task | Start Date | Completion Date | Reference Material |
| :--- | :--- | :--- | :--- | :--- |
| Saturday (on-site) | Design NetworkDevices with deviceId (String) as its partition key. | 19/09/2026 | 19/09/2026 | [Amazon DynamoDB](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/Introduction.html) |
| Sunday (independent study) | Agree on deviceName, deviceType, ipAddress, location, status, cpuUsage, memoryUsage, and lastUpdated. | 20/09/2026 | 20/09/2026 | [Amazon DynamoDB](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/Introduction.html) |
| Monday (independent study) | Outline NetworkAlerts with eventId, alarmName, alarmState, eventTime, and handlingStatus. | 21/09/2026 | 21/09/2026 | [Amazon DynamoDB](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/Introduction.html) |
| Tuesday (independent study) | Inspect items in Explore table items and distinguish String, Number, and Python Decimal values. | 22/09/2026 | 22/09/2026 | [Boto3 DynamoDB Table](https://boto3.amazonaws.com/v1/documentation/api/latest/reference/services/dynamodb/table/index.html) |

### Week 5 Achievements:

- Defined a shared **NetworkDevices** schema and device-based partition key.
- Prepared **NetworkAlerts** to record alarm times and handling states.
- Learned to verify writes using **Explore table items** rather than trusting the frontend alone.

