---
title: "5.6.3. Clean Up CloudWatch, SNS, and EventBridge"
date: 2026-11-11T00:00:00+07:00
draft: false
weight: 3
---

# 5.6.3. Clean Up CloudWatch, SNS, and EventBridge

## When to do this

**Only clean up after the demo is complete and all evidence has been backed up.** Do not delete alarms, SNS topics, or EventBridge rules if alerting is still required.

## Cleanup steps

1. Open **CloudWatch → Alarms** and capture the settings/history of `netmon-cpu-high-80`, `netmon-ram-high-80`, and `netmon-disk-high-85`.

{{< netmonimg src="images/netmon-workshop/21-cloudwatch-alarms-list.png" alt="Three CloudWatch alarms" caption="Figure 21 – Three CloudWatch alarms" >}}

2. Delete alarms individually only after their monitoring purpose has ended. This stops alarm evaluation; it does not delete EC2.

3. Open **EventBridge → Event buses → default → Rules**, inspect `netmon-alarm-state-rule` and its targets, then delete the rule if unused.

{{< netmonimg src="images/netmon-workshop/28-eventbridge-default-bus-rule-enabled.png" alt="EventBridge default bus and rule" caption="Figure 28 – EventBridge default bus and rule" >}}

4. Open **SNS → Topics → `netmon-alerts`**; record the subscriptions and remove the topic only after email testing has ended.

{{< netmonimg src="images/netmon-workshop/26-sns-subscriptions-confirmed-list.png" alt="SNS subscription list" caption="Figure 26 – SNS subscription list" >}}


5. Inspect **CloudWatch → Log groups**, export logs needed for the report, and remove disposable test log groups.

## Verification

Use exact resource names and verify every removal to avoid deleting unrelated resources in the same AWS account.

---

> **Publishing note:** Do not publish original images showing email addresses, login codes, or tokens. Screenshots in this pack come from the lab and have the account header removed; review them again before going public.

[← Back to chapter](../)
