---
title: "5.3.2. Create CloudWatch Alarms and SNS Email"
date: 2026-11-11T00:00:00+07:00
draft: false
weight: 2
---

# 5.3.2. Create CloudWatch Alarms and SNS Email

## Objective

Create CPU, memory, and disk alarms and use SNS to send notifications when configured thresholds are exceeded.

## Create an SNS Topic

1. Go to **Amazon SNS → Topics → Create topic**, select Standard, and name it `netmon-alerts`.
2. Open the topic and choose **Create subscription**. Select `Email` and provide the recipient address.

3. Open the AWS SNS confirmation message and select **Confirm subscription**. A `Pending confirmation` subscription cannot receive notifications.

{{< netmonimg src="images/netmon-workshop/25-sns-new-subscription-confirmed.png" alt="Confirmed SNS subscription" caption="Figure 25 – Confirmed SNS subscription" >}}


{{< netmonimg src="images/netmon-workshop/26-sns-subscriptions-confirmed-list.png" alt="SNS subscription list" caption="Figure 26 – SNS subscription list" >}}


{{< netmonimg src="images/netmon-workshop/27-sns-netmon-alerts-new-email-confirmed.png" alt="SNS netmon-alerts with confirmed email" caption="Figure 27 – SNS netmon-alerts with confirmed email" >}}


4. Use **Publish message** to send a test message; check Inbox and Spam. The group previously confirmed successful test email delivery.

## CloudWatch alarms

| Alarm | Metric | Lab threshold |
|---|---|---|
| `netmon-cpu-high-80` | `AWS/EC2 / CPUUtilization` | Greater than 80% |
| `netmon-ram-high-80` | `NetMon/EC2 / mem_used_percent` | Greater than 80% |
| `netmon-disk-high-85` | `NetMon/EC2 / disk_used_percent` | Greater than 85% |

For each one, select **CloudWatch → Alarms → Create alarm → Select metric**. Choose **Average**, **5 minutes**, **1 out of 1 datapoint**, and send the `In alarm` notification to `netmon-alerts`. These values are lab settings, not universal operational thresholds.

## Verification

In **CloudWatch → Alarms**, review all three alarms and their `OK`, `ALARM`, or `INSUFFICIENT_DATA` state. An `OK` state only indicates that the monitored metric is not breaching at that moment; it does not prove the entire SNS or EventBridge flow works.

---

> **Publishing note:** Do not publish original images showing email addresses, login codes, or tokens. Screenshots in this pack come from the lab and have the account header removed; review them again before going public.

## Related evidence screenshots

{{< netmonimg src="images/netmon-workshop/21-cloudwatch-alarms-list.png" alt="Three CloudWatch alarms" caption="Figure 21 – Three CloudWatch alarms" >}}

{{< netmonimg src="images/netmon-workshop/22-cloudwatch-disk-high-85-details.png" alt="Disk usage alarm at 85%" caption="Figure 22 – Disk usage alarm at 85%" >}}

{{< netmonimg src="images/netmon-workshop/23-cloudwatch-ram-high-80-details.png" alt="RAM usage alarm at 80%" caption="Figure 23 – RAM usage alarm at 80%" >}}

{{< netmonimg src="images/netmon-workshop/24-cloudwatch-cpu-high-80-details.png" alt="CPU usage alarm at 80%" caption="Figure 24 – CPU usage alarm at 80%" >}}

[← Back to chapter](../)
