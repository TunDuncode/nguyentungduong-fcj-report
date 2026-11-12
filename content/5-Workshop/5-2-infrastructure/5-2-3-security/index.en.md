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

{{< netmonimg src="images/netmon-workshop/15-security-groups-list.png" alt="Security-group list" caption="Figure 15 – Security-group list" >}}


{{< netmonimg src="images/netmon-workshop/16-netmon-ec2-sg-inbound-no-rules.png" alt="Empty inbound rules of netmon-ec2-sg" caption="Figure 16 – Empty inbound rules of netmon-ec2-sg" >}}


{{< netmonimg src="images/netmon-workshop/17-netmon-ec2-sg-outbound-all-traffic.png" alt="Outbound rules of netmon-ec2-sg" caption="Figure 17 – Outbound rules of netmon-ec2-sg" >}}


{{< netmonimg src="images/netmon-workshop/20-ec2-security-netmon-ec2-sg.png" alt="EC2 security tab" caption="Figure 20 – EC2 security tab" >}}



3. If using **AWS Systems Manager Session Manager**, verify the SSM Agent, IAM instance profile, and required network connectivity; otherwise use another restricted administration path.
4. Use **EC2 → Actions → Security → Modify IAM role** to attach a suitable profile for publishing CloudWatch Agent metrics.

5. Verify the instance health and monitoring data in EC2 and CloudWatch.

## Verification

- Inbound rules match the demo's requirements and do not expose SSH globally.
- Use an IAM role rather than storing AWS Access Keys on the server.
- Check that administrative access works and can be revoked.

---

> **Publishing note:** Do not publish original images showing email addresses, login codes, or tokens. Screenshots in this pack come from the lab and have the account header removed; review them again before going public.

[← Back to chapter](../)
