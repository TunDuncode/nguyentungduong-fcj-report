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
2. Delete alarms individually only after their monitoring purpose has ended. This stops alarm evaluation; it does not delete EC2.

![Three CloudWatch alarms after creation]({{< relURL "images/netmon-workshop/cloudwatch-alarms.webp" >}})

*Evidence: Three CloudWatch alarms after creation. Captured during the NetMon lab; the AWS account header has been removed.*

3. Open **EventBridge → Event buses → default → Rules**, inspect `netmon-alarm-state-rule` and its targets, then delete the rule if unused.
4. Open **SNS → Topics → `netmon-alerts`**; record the subscriptions and remove the topic only after email testing has ended.

![NetMon EventBridge rule]({{< relURL "images/netmon-workshop/eventbridge-rule.webp" >}})

*Evidence: NetMon EventBridge rule. Captured during the NetMon lab; the AWS account header has been removed.*

5. Inspect **CloudWatch → Log groups**, export logs needed for the report, and remove disposable test log groups.

## Verification

Use exact resource names and verify every removal to avoid deleting unrelated resources in the same AWS account.

---

> **Publishing note:** Do not publish original images showing email addresses, login codes, or tokens. Screenshots in this pack come from the lab and have the account header removed; review them again before going public.

[← Back to chapter](../)
