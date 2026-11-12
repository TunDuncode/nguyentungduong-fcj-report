---
title: "5.3.3. Route Alarm Changes with EventBridge"
date: 2026-11-11T00:00:00+07:00
draft: false
weight: 3
---

# 5.3.3. Route Alarm Changes with EventBridge

## Objective

When a CloudWatch Alarm changes state, EventBridge invokes a Lambda function that stores alert history in DynamoDB for time tracking and incident handling.

## Steps

1. Ensure that the `NetworkAlerts` table exists with String partition key `eventId`.
2. Create the Python Lambda `netmon-save-alert` and give its execution role `dynamodb:PutItem` on the `NetworkAlerts` table and CloudWatch Logs permissions.

![EventBridge CloudWatch event pattern]({{< relURL "images/netmon-workshop/eventbridge-pattern.webp" >}})

*Evidence: EventBridge CloudWatch event pattern. Captured during the NetMon lab; the AWS account header has been removed.*

3. Open **Amazon EventBridge → Event buses → default → Rules → Create rule**. Name it `netmon-alarm-state-rule` on the `default` event bus.

![Choose Lambda as an EventBridge target]({{< relURL "images/netmon-workshop/eventbridge-target.webp" >}})

*Evidence: Choose Lambda as an EventBridge target. Captured during the NetMon lab; the AWS account header has been removed.*

4. Choose **Custom pattern (JSON editor)** and enter:

```json
{
  "source": ["aws.cloudwatch"],
  "detail-type": ["CloudWatch Alarm State Change"],
  "detail": {
    "alarmName": [
      "netmon-cpu-high-80",
      "netmon-ram-high-80",
      "netmon-disk-high-85"
    ]
  }
}
```

5. Set the **Target** to `netmon-save-alert`. Verify that the Lambda resource-based policy allows EventBridge invocation.

![NetMon EventBridge rule]({{< relURL "images/netmon-workshop/eventbridge-rule.webp" >}})

*Evidence: NetMon EventBridge rule. Captured during the NetMon lab; the AWS account header has been removed.*

6. Test with a valid CloudWatch event or a controlled alarm state change in the demo environment. Then open **DynamoDB → Explore items → NetworkAlerts → Scan → Run**.

## Verification

Records should include fields such as `eventId`, `alarmName`, `alarmState`, `eventTime`, and device identification where available. Distinguish test records from genuine events using `isTest`. Earlier lab results showed one test record (`isTest=true`) and a non-test event (`isTest=false`).

> Common issue: `AccessDeniedException` for `dynamodb:PutItem`. Fix the execution role policy and retry; do not recreate the table to work around an IAM issue.

![NetMon architecture diagram]({{< relURL "images/netmon-workshop/netmon-alert-flow.png" >}})

---

> **Publishing note:** Do not publish original images showing email addresses, login codes, or tokens. Screenshots in this pack come from the lab and have the account header removed; review them again before going public.

[← Back to chapter](../)
