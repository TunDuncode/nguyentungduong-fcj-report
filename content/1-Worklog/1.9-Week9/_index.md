---
title: "Week 9 Worklog"
date: 2026-06-15
weight: 9
chapter: false
pre: " <b> 1.9. </b> "
---



### Week 9 Objectives:

* Deploy an isolated managed cloud database server deep within private internal networks.
* Establish secure multi-tier communication links between compute applications and data tiers (Lab 5).

### Tasks to be carried out this week:
| Day | Task | Start Date | Completion Date | Reference Material |
| --- | --- | --- | --- | --- |
| 7   | - Research safe network group configurations for DB layer <br>&emsp; + Formulate DB Subnet Groups isolated inside Private Subnets | 03/10/2026 | 03/10/2026      | <https://cloudjourney.awsstudygroup.com/> |
| sunday   | - Configure firewall rules guarding the Database layer <br>&emsp; + Create DB Security Groups <br>&emsp; + Allow inbound traffic exclusively from the Web/App Security Group | 04/10/2026 | 04/10/2026      | <https://cloudjourney.awsstudygroup.com/> |
| 2   | - **Practice (Part 1):** <br>&emsp; + Provision an Amazon RDS MySQL Instance using Free Tier allocations <br>&emsp; + Bind prepared DB Subnet Groups and Security Groups to the instance | 05/10/2026 | 05/10/2026      | <https://cloudjourney.awsstudygroup.com/> |
| 3   | - **Practice (Part 2):** <br>&emsp; + Connect securely via SSH into the EC2 Bastion Host compute environment <br>&emsp; + Install native MySQL CLI tools locally onto the EC2 host | 06/10/2026 | 06/10/2026      | <https://cloudjourney.awsstudygroup.com/> |
| 4   | - **Practice (Part 3):** <br>&emsp; + Establish an internal link from EC2 to the RDS Endpoint <br>&emsp; + Run basic SQL operations (CREATE TABLE, INSERT, SELECT) <br>&emsp; + Tear down resources to avoid extra costs | 07/10/2026 | 07/10/2026      | <https://cloudjourney.awsstudygroup.com/> |


### Week 9 Achievements:

* Successfully established and operated a multi-tier secure infrastructure topology:
  * Positioned data processing layers completely inside private internal subnet zones.
  * Blocked external malicious connection attempts originating from public internet areas.
  * ...

* Mastered precise firewall management configurations for critical database layers:
  * Created operational mappings connecting DB Subnet Groups across disparate availability sectors.
  * Enforced inbound rules restricting connections solely to standard database ports (Port 3306) from specified app engines.
  * ...

* Solidified terminal command-line operations to maintain cloud services remotely:
  * Handled Linux server environments effectively to communicate with managed cloud infrastructure.
  * Completed database table writing and query validation checks successfully using the native MySQL CLI.
  * ...

* Recognized resource allocation responsibilities by completing cleanup procedures to preserve account credit.
* ...