---
title: "Week 11 Worklog"
date: 2026-06-29
weight: 11
chapter: false
pre: " <b> 1.11. </b> "
---


### Week 11 Objectives:

* Deploy a resilient system architecture capable of automated scaling and load balancing.
* Implement a connected Application Load Balancer and Auto Scaling Group across multiple zones (Lab 6).

### Tasks to be carried out this week:
| Day | Task | Start Date | Completion Date | Reference Material |
| --- | --- | --- | --- | --- |
| 7   | - **Practice (Part 1):** <br>&emsp; + Create an EC2 Launch Template blueprint <br>&emsp; + Input shell script into User Data to pre-install Apache servers | 17/10/2026 | 17/10/2026      | <https://cloudjourney.awsstudygroup.com/> |
| sunday   | - **Practice (Part 2):** <br>&emsp; + Build a Target Group mapping HTTP traffic on Port 80 <br>&emsp; + Launch a public-facing Application Load Balancer (ALB) | 18/10/2026 | 18/10/2026      | <https://cloudjourney.awsstudygroup.com/> |
| 2   | - **Practice (Part 3):** <br>&emsp; + Initialize an Auto Scaling Group (ASG) linked to the Launch Template <br>&emsp; + Distribute the ASG footprint across 2 distinct Availability Zones | 19/10/2026 | 19/10/2026      | <https://cloudjourney.awsstudygroup.com/> |
| 3   | - **Practice (Part 4):** <br>&emsp; + Define capacity boundaries: Desired = 2, Min = 2, Max = 4 instances <br>&emsp; + Register the ASG cluster with the active ALB Health Check trackers | 20/10/2026 | 20/10/2026      | <https://cloudjourney.awsstudygroup.com/> |
| 4   | - **Practice (Part 5):** <br>&emsp; + Simulate a disaster scenario by terminating a running instance manually <br>&emsp; + Monitor the system detecting failure and provisioning a replacement <br>&emsp; + Clean up systems | 21/10/2026 | 21/10/2026      | <https://cloudjourney.awsstudygroup.com/> |


### Week 11 Achievements:

* Successfully constructed and validated a Self-healing cloud infrastructure layout:
  * Automated application server staging routines cleanly using shell script configurations within User Data blocks.
  * Channeled incoming connection pathways evenly to background computing targets via a singular ALB DNS endpoint.
  * ...

* Realized full system disaster recovery planning at a data center scale:
  * Protected service availability lines by stretching virtual server footprints across physical Availability Zone boundaries.
  * Confirmed backup zones automatically absorb standard visitor loads if one data sector becomes isolated.
  * ...

* Demonstrated elastic performance capabilities built into active Auto Scaling Groups:
  * Verified systems correctly identify drops below Desired Capacity levels when instances face sudden destruction.
  * Monitored the automated launch, verification checks, and configuration integration of fresh servers without human interaction.
  * ...

* Formulated resource collection management procedures to terminate multi-tier scaling stacks cleanly.
* ...