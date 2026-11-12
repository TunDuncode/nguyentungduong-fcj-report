---
title: "5.3.4. Store Alert History with Lambda and DynamoDB"
date: 2026-11-11T00:00:00+07:00
draft: false
weight: 4
---

# 5.3.4. Store Alert History with Lambda and DynamoDB

## Goal

Store **CloudWatch Alarm State Change** events in `NetworkAlerts`, tracking occurrence time and whether the incident has been handled.

## Console steps

1. Open **DynamoDB → Tables** and verify `NetworkAlerts`, with String partition key `eventId`.
2. Open **Lambda → Functions → `netmon-save-alert`**. Deploy code that parses `event.detail.alarmName`, `event.detail.state.value`, `event.id`, and the event timestamp.

![Lambda test before permissions were corrected]({{< relURL "images/netmon-workshop/lambda-test-error.webp" >}})

*Evidence: Lambda test before permissions were corrected. Captured during the NetMon lab; the AWS account header has been removed.*

3. Under **Configuration → Permissions**, grant the execution role **`dynamodb:PutItem`** to the `NetworkAlerts` table ARN, plus CloudWatch Logs permissions.

![Lambda tested after updating permissions]({{< relURL "images/netmon-workshop/lambda-test-ok.webp" >}})

*Evidence: Lambda tested after updating permissions. Captured during the NetMon lab; the AWS account header has been removed.*

4. Run a representative EventBridge test event. An `AccessDeniedException` for `PutItem` means the **Lambda execution role** needs correction.
5. Open **DynamoDB → Explore items → NetworkAlerts → Scan → Run** to inspect the stored item.

![NetworkAlerts stores event history]({{< relURL "images/netmon-workshop/dynamodb-alerts-two.webp" >}})

*Evidence: NetworkAlerts stores event history. Captured during the NetMon lab; the AWS account header has been removed.*

6. Inspect `eventId`, `alarmName`, `alarmState`, `eventTime`, `handlingStatus`, and `isTest`. Do not mark alerts as handled before action is taken.

## Observed result

The team’s screenshots show a test item named `netmon-test-001` and at least one item with `isTest=false` in `NetworkAlerts`. This demonstrates event storage, but does not prove that every alarm was triggered by real load.

---

> **Publishing note:** Do not publish original images showing email addresses, login codes, or tokens. Screenshots in this pack come from the lab and have the account header removed; review them again before going public.

[← Back to chapter](../)
