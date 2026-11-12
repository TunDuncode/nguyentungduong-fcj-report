---
title: "5.2.2. Launch an Ubuntu EC2 Instance"
date: 2026-11-11T00:00:00+07:00
draft: false
weight: 2
---

# 5.2.2. Launch an Ubuntu EC2 Instance

## Objective

Launch an Ubuntu server for CloudWatch monitoring tests while reducing unauthorized-access risks.

## Steps

1. Open **EC2 → Instances → Launch instances**.
2. Set the instance name to `netmon-ec2-server`, matching the lab naming convention.
3. Choose **Ubuntu Server 24.04 LTS** and an instance type appropriate to the available budget and usage limits.

![EC2 instance creation and configuration]({{< relURL "images/netmon-workshop/ec2-creation.webp" >}})

*Evidence: EC2 instance creation and configuration. Captured during the NetMon lab; the AWS account header has been removed.*

4. In **Network settings**, select the intended VPC and public subnet and review public IP assignment.

![Options while configuring an EC2 instance]({{< relURL "images/netmon-workshop/ec2-security.webp" >}})

*Evidence: Options while configuring an EC2 instance. Captured during the NetMon lab; the AWS account header has been removed.*

5. Configure the **Security Group**: do not allow SSH port `22` from `0.0.0.0/0`. Restrict SSH to trusted administrator addresses or use Systems Manager Session Manager when supported.

![EC2 instance shown in the Instances list]({{< relURL "images/netmon-workshop/ec2-list.webp" >}})

*Evidence: EC2 instance shown in the Instances list. Captured during the NetMon lab; the AWS account header has been removed.*

6. Keep EBS storage appropriately sized; EBS can still incur costs after an instance is stopped.
7. Launch the instance and wait for the EC2 status checks to pass. Attach an IAM instance profile if CloudWatch Agent requires access to publish metrics or logs.

## Verification

- The instance is `Running` when monitoring is needed.
- CloudWatch shows CPUUtilization for the correct InstanceId.
- Capture the instance name, type, subnet, Security Group, and status checks (redact details you do not wish to publish).

> Stopping EC2 generally stops running compute charges, but not necessarily EBS or public IPv4 charges.

---

> **Publishing note:** Do not publish original images showing email addresses, login codes, or tokens. Screenshots in this pack come from the lab and have the account header removed; review them again before going public.

[← Back to chapter](../)
