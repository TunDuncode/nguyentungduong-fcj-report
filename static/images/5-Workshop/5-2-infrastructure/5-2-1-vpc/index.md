---
title: "5.2.1. Create a VPC, Subnets, Routes, and IGW"
date: 2026-11-11T00:00:00+07:00
draft: false
weight: 1
---

# 5.2.1. Create a VPC, Subnets, Routes, and IGW

## Objective

Build a virtual network for the monitored EC2 instance, separating Internet-facing and internal resources.

## AWS Console steps

1. Go to **VPC → Your VPCs → Create VPC**. Choose an appropriate configuration. Example lab CIDR: `10.0.0.0/16` (not a claim about the team's actual CIDR).
2. Create a **public subnet** (e.g., `10.0.1.0/24`) and a **private subnet** (e.g., `10.0.2.0/24`) in the appropriate Availability Zone.
3. Create an **Internet Gateway** and attach it to the VPC.

![EC2 instance creation and configuration]({{< relURL "images/netmon-workshop/ec2-creation.webp" >}})

*Evidence: EC2 instance creation and configuration. Captured during the NetMon lab; the AWS account header has been removed.*

4. Create a **public route table**, add `0.0.0.0/0` pointing to the Internet Gateway, and associate it with the public subnet.
5. A private subnet has no automatic Internet access. If outbound Internet access is required, design NAT appropriately and consider the cost before creating it.
6. Review **Network ACLs** and **Security Groups** against the required traffic flows and deny unnecessary access.

## Evidence to capture

- VPC, CIDR ranges, and subnet list.
- Route table and Internet Gateway association.
- Security Group attached to EC2.

> Do not create a NAT Gateway solely for screenshots. It can incur hourly and data-processing charges.

![Illustrative workflow diagram]({{< relURL "images/netmon-workshop/netmon-vpc-flow.png" >}})

---

> **Publishing note:** Do not publish original images showing email addresses, login codes, or tokens. Screenshots in this pack come from the lab and have the account header removed; review them again before going public.

[← Back to chapter](../)
