---
title: "5.3.1. Collect CPU, RAM, and Disk Metrics"
date: 2026-11-11T00:00:00+07:00
draft: false
weight: 1
---

# 5.3.1. Collect CPU, RAM, and Disk Metrics

## Objective

Publish EC2 CPU, memory, and disk utilization metrics to CloudWatch for monitoring and alert evaluation.

## Steps

1. Open **CloudWatch → Metrics → All metrics** and find `AWS/EC2 → CPUUtilization` for the target InstanceId. CPU is an EC2 standard metric.
2. For memory and disk, install and configure **Amazon CloudWatch Agent** on Ubuntu. The instance role must permit metric publishing, for example through suitable `CloudWatchAgentServerPolicy` permissions.

![Install CloudWatch Agent with Systems Manager Run Command]({{< relURL "images/netmon-workshop/ec2-role.webp" >}})

*Evidence: Install CloudWatch Agent with Systems Manager Run Command. Captured during the NetMon lab; the AWS account header has been removed.*

3. Configure the agent to collect `mem_used_percent` and `disk_used_percent` with consistent namespace and dimensions. The team's monitoring screenshots used **`NetMon/EC2`** as the custom namespace.

![The group’s CloudWatch monitoring page]({{< relURL "images/netmon-workshop/cloudwatch-dashboard.webp" >}})

*Evidence: The group’s CloudWatch monitoring page. Captured during the NetMon lab; the AWS account header has been removed.*

4. Locate the custom metrics in CloudWatch. Memory metrics may use InstanceId, while disk metrics can additionally include `path`, `device`, and `fstype`.

![CloudWatch metric chart]({{< relURL "images/netmon-workshop/cloudwatch-metric.webp" >}})

*Evidence: CloudWatch metric chart. Captured during the NetMon lab; the AWS account header has been removed.*

5. For the alarm configuration, select `Statistic: Average` and `Period: 5 minutes`, matching the lab settings.

## Why memory/disk differ from CPU

The standard EC2 metrics do not include operating-system-level memory and filesystem usage percentages. CloudWatch Agent needs to run and publish these values.

## Verification

- A CPUUtilization graph exists under `AWS/EC2`.
- `mem_used_percent` and `disk_used_percent` show recent datapoints under the selected namespace.
- If the graph says **No data available**, check the agent, IAM role, Region, and dimension combinations before creating alarms.

---

> **Publishing note:** Do not publish original images showing email addresses, login codes, or tokens. Screenshots in this pack come from the lab and have the account header removed; review them again before going public.

[← Back to chapter](../)
