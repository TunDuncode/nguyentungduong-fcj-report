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

1. Go to **VPC → Your VPCs → Create VPC**. Choose an appropriate configuration. observed VPC CIDR `10.0.0.0/16`.

{{< netmonimg src="images/netmon-workshop/06-netmon-vpc-resource-map.png" alt="netmon-vpc resource map" caption="Figure 06 – netmon-vpc resource map" >}}

2. Create a **public subnet** (e.g., `10.0.0.0/20`) and a **private subnet** (e.g., `10.0.128.0/20`) in the appropriate Availability Zone.

{{< netmonimg src="images/netmon-workshop/07-subnet-list.png" alt="List of two subnets" caption="Figure 07 – List of two subnets" >}}


{{< netmonimg src="images/netmon-workshop/08-public-subnet-details.png" alt="Public subnet details" caption="Figure 08 – Public subnet details" >}}


{{< netmonimg src="images/netmon-workshop/09-private-subnet-details.png" alt="Private subnet details" caption="Figure 09 – Private subnet details" >}}

3. Create an **Internet Gateway** and attach it to the VPC.

{{< netmonimg src="images/netmon-workshop/14-netmon-igw-details.png" alt="netmon-igw internet gateway" caption="Figure 14 – netmon-igw internet gateway" >}}


4. Create a **public route table**, add `0.0.0.0/0` pointing to the Internet Gateway, and associate it with the public subnet.

{{< netmonimg src="images/netmon-workshop/10-route-tables-list.png" alt="Route-table list" caption="Figure 10 – Route-table list" >}}


{{< netmonimg src="images/netmon-workshop/11-netmon-rtb-public-routes.png" alt="Routes in netmon-rtb-public" caption="Figure 11 – Routes in netmon-rtb-public" >}}


{{< netmonimg src="images/netmon-workshop/12-netmon-main-route-table-no-name.png" alt="VPC main route table" caption="Figure 12 – VPC main route table" >}}


{{< netmonimg src="images/netmon-workshop/13-netmon-rtb-private1-us-east-1a-routes.png" alt="Private subnet route table" caption="Figure 13 – Private subnet route table" >}}

5. A private subnet has no automatic Internet access. If outbound Internet access is required, design NAT appropriately and consider the cost before creating it.
6. Review **Network ACLs** and **Security Groups** against the required traffic flows and deny unnecessary access.

## Evidence to capture

- VPC, CIDR ranges, and subnet list.
- Route table and Internet Gateway association.
- Security Group attached to EC2.

> Do not create a NAT Gateway solely for screenshots. It can incur hourly and data-processing charges.

---

> **Publishing note:** Do not publish original images showing email addresses, login codes, or tokens. Screenshots in this pack come from the lab and have the account header removed; review them again before going public.

[← Back to chapter](../)
