---
title: "5.2.3. Security Groups, IAM Roles, and Safe Access"
date: 2026-11-11T00:00:00+07:00
draft: false
weight: 3
---

# 5.2.3. Security Groups, IAM Roles, and Safe Access

## Goal

Protect `netmon-ec2-server` and enable monitoring without exposing management ports to the entire Internet.

## Console steps

1. Open **EC2 → Instances**, select `netmon-ec2-server`, and open **Security**.
2. Inspect the attached **Security Group → Inbound rules**. Do not expose TCP/22 to `0.0.0.0/0` without a justified, reviewed need.

![Choose a safe EC2 connection method]({{< relURL "images/netmon-workshop/ec2-ssm.webp" >}})

*Evidence: Choose a safe EC2 connection method. Captured during the NetMon lab; the AWS account header has been removed.*

3. If using **AWS Systems Manager Session Manager**, verify the SSM Agent, IAM instance profile, and required network connectivity; otherwise use another restricted administration path.
4. Use **EC2 → Actions → Security → Modify IAM role** to attach a suitable profile for publishing CloudWatch Agent metrics.

![Options while configuring an EC2 instance]({{< relURL "images/netmon-workshop/ec2-security.webp" >}})

*Evidence: Options while configuring an EC2 instance. Captured during the NetMon lab; the AWS account header has been removed.*

5. Verify the instance health and monitoring data in EC2 and CloudWatch.

## Verification

- Inbound rules match the demo's requirements and do not expose SSH globally.
- Use an IAM role rather than storing AWS Access Keys on the server.
- Check that administrative access works and can be revoked.

---

> **Publishing note:** Do not publish original images showing email addresses, login codes, or tokens. Screenshots in this pack come from the lab and have the account header removed; review them again before going public.

[← Back to chapter](../)
