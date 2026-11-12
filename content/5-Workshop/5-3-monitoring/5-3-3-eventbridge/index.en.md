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

3. Open **Amazon EventBridge → Event buses → default → Rules → Create rule**. Name it `netmon-alarm-state-rule` on the `default` event bus.

{{< netmonimg src="images/netmon-workshop/28-eventbridge-default-bus-rule-enabled.png" alt="EventBridge default bus and rule" caption="Figure 28 – EventBridge default bus and rule" >}}


4. Choose **Custom pattern (JSON editor)** and enter:

{{< netmonimg src="images/netmon-workshop/29-eventbridge-netmon-alarm-state-rule-pattern.png" alt="CloudWatch alarm event pattern" caption="Figure 29 – CloudWatch alarm event pattern" >}}


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

{{< netmonimg src="images/netmon-workshop/30-eventbridge-netmon-alarm-state-rule-lambda-target.png" alt="EventBridge Lambda target" caption="Figure 30 – EventBridge Lambda target" >}}


6. Test with a valid CloudWatch event or a controlled alarm state change in the demo environment. Then open **DynamoDB → Explore items → NetworkAlerts → Scan → Run**.

## Verification

Records should include fields such as `eventId`, `alarmName`, `alarmState`, `eventTime`, and device identification where available. Distinguish test records from genuine events using `isTest`. Earlier lab results showed one test record (`isTest=true`) and a non-test event (`isTest=false`).

> Common issue: `AccessDeniedException` for `dynamodb:PutItem`. Fix the execution role policy and retry; do not recreate the table to work around an IAM issue.


---

> **Publishing note:** Do not publish original images showing email addresses, login codes, or tokens. Screenshots in this pack come from the lab and have the account header removed; review them again before going public.

[← Back to chapter](../)
