---
title: "4. Ubuntu EC2, EBS, and basic monitoring"
date: 2026-09-12T09:00:00+07:00
weight: 4
draft: false
description: "Ubuntu EC2, EBS, and basic monitoring"
---

# 4. Ubuntu EC2, EBS, and basic monitoring

### Week 4 Objectives:

- Understand how the NetMon team provisions EC2.
- Learn the roles of AMIs, instance types, EBS, and IAM Roles.
- Distinguish default EC2 CPU metrics from RAM/disk metrics requiring the CloudWatch Agent.

### Tasks to be carried out this week:

| Day | Task | Start Date | Completion Date | Reference Material |
| :--- | :--- | :--- | :--- | :--- |
| Saturday (on-site) | Follow Tùng Dương’s configuration of netmon-ec2-server using Ubuntu 24.04 LTS. | 12/09/2026 | 12/09/2026 | [Amazon EC2](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/concepts.html) |
| Sunday (independent study) | Review root EBS volumes, Security Groups, instance state, and displayed status checks. | 13/09/2026 | 13/09/2026 | [Amazon EBS](https://docs.aws.amazon.com/ebs/latest/userguide/what-is-ebs.html) |
| Monday (independent study) | Review attaching an IAM Role after launch and locating EC2 metrics in CloudWatch. | 14/09/2026 | 14/09/2026 | [Amazon EC2](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/concepts.html) |
| Tuesday (independent study) | Discuss associating device records with EC2 using instanceId, region, and monitoringSource. | 15/09/2026 | 15/09/2026 | [Amazon DynamoDB](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/Introduction.html) |

### Week 4 Achievements:

- Understood provisioning and cost considerations for **netmon-ec2-server**.
- Learned that CPUUtilization is available by default while RAM/disk require additional collection depending on setup.
- Agreed to label simulated and real EC2 metrics separately.

