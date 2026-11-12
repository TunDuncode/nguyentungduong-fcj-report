---
title: "3. VPC network design and infrastructure separation"
date: 2026-09-05T09:00:00+07:00
weight: 3
draft: false
description: "VPC network design and infrastructure separation"
---

# 3. VPC network design and infrastructure separation

### Week 3 Objectives:

- Read a basic VPC topology.
- Understand public/private subnets, route tables, and Internet Gateway.
- Explain how the Serverless backend complements the team’s EC2 infrastructure.

### Tasks to be carried out this week:

| Day | Task | Start Date | Completion Date | Reference Material |
| :--- | :--- | :--- | :--- | :--- |
| Saturday (on-site) | Review the netmon-vpc topology and test CIDR range with Tùng Dương. | 05/09/2026 | 05/09/2026 | [Amazon VPC](https://docs.aws.amazon.com/vpc/latest/userguide/what-is-amazon-vpc.html) |
| Sunday (independent study) | Distinguish public and private subnets and routes to the Internet Gateway. | 06/09/2026 | 06/09/2026 | [Amazon VPC](https://docs.aws.amazon.com/vpc/latest/userguide/what-is-amazon-vpc.html) |
| Monday (independent study) | Study Security Group ingress/egress and why SSH port 22 should not be publicly exposed. | 07/09/2026 | 07/09/2026 | [Security Groups](https://docs.aws.amazon.com/vpc/latest/userguide/vpc-security-groups.html) |
| Tuesday (independent study) | Sketch separate Dashboard → API Gateway → Lambda → DynamoDB and EC2 → CloudWatch flows. | 08/09/2026 | 08/09/2026 | [Amazon VPC](https://docs.aws.amazon.com/vpc/latest/userguide/what-is-amazon-vpc.html) |

### Week 3 Achievements:

- Understood the simulated network architecture and Serverless integration flow.
- Distinguished **EC2 metrics** from simulated device readings stored in **NetworkDevices**.
- Kept VPC/EC2 ownership with Tùng Dương while preparing the API integration.

