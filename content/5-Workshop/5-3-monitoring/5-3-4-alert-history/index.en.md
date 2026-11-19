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

{{< netmonimg src="images/netmon-workshop/31-lambda-netmon-save-alert-code-overview.png" alt="netmon-save-alert Lambda code" caption="Figure 31 – netmon-save-alert Lambda code" >}}

3. Under **Configuration → Permissions**, grant the execution role **`dynamodb:PutItem`** to the `NetworkAlerts` table ARN, plus CloudWatch Logs permissions.

4. Run a representative EventBridge test event. An `AccessDeniedException` for `PutItem` means the **Lambda execution role** needs correction.
5. Open **DynamoDB → Explore items → NetworkAlerts → Scan → Run** to inspect the stored item.

{{< netmonimg src="images/netmon-workshop/32-dynamodb-networkalerts-7-items.png" alt="Items in NetworkAlerts" caption="Figure 32 – Items in NetworkAlerts" >}}

6. Inspect `eventId`, `alarmName`, `alarmState`, `eventTime`, `handlingStatus`, and `isTest`. Do not mark alerts as handled before action is taken.

## Observed result

The team’s screenshots show a test item named `netmon-test-001` and at least one item with `isTest=false` in `NetworkAlerts`. This demonstrates event storage, but does not prove that every alarm was triggered by real load.

## Display and handle alerts in NetMon

`GET /alerts` reads history; `PUT /alerts/{id}` updates handling status. `alarmState` represents the monitoring state (`ALARM`, `OK`, `INSUFFICIENT_DATA`), whereas `handlingStatus` represents an administrator's response. The fields are independent. The demo UI sends `Resolved`; reconcile it with the backend if older records use `New` or `Handled`, rather than overwriting history.

In the alert center, inspect the device, alert type, and timestamp, confirm handling, then reload the list. If the state changes only in the browser but not in DynamoDB, check the HTTP response and write permission. Local UI action logs, where present, do not replace AWS history.


[← Back to chapter](../)
