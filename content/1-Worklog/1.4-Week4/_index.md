---
title: "Week 4 Worklog"
date: 2026-05-11
weight: 4
chapter: false
pre: " <b> 1.4. </b> "
---




### Week 4 Objectives:

* Explore Database services on AWS.
* Differentiate between relational databases (RDS) and non-relational databases (NoSQL).

### Tasks to be carried out this week:
| Day | Task | Start Date | Completion Date | Reference Material |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | --------------- | ----------------------------------------- |
| 7   | - Learn Amazon RDS (Relational DB) <br>&emsp; + MySQL, PostgreSQL <br>&emsp; + Multi-AZ Deployments <br>&emsp; + Read Replicas <br> | 29/08/2026   | 29/08/2026      | <https://cloudjourney.awsstudygroup.com/> |
| sunday   | - Learn Amazon DynamoDB (NoSQL DB) <br>&emsp; + Partition Keys <br>&emsp; + Sort Keys <br>&emsp; + Provisioned vs On-demand <br> | 30/08/2026   | 30/08/2026      | <https://cloudjourney.awsstudygroup.com/> |
| 2   | - Analyze Use-cases for RDS and DynamoDB <br> - Learn to design DB Subnet Groups <br> | 31/08/2026   | 31/08/2026      | <https://cloudjourney.awsstudygroup.com/> |
| 3   | - **Practice:** <br>&emsp; + Configure Private Subnet for DB <br>&emsp; + Create DB Security Group (only allow traffic from EC2) <br> | 01/09/2026   | 01/09/2026      | <https://cloudjourney.awsstudygroup.com/> |
| 4   | - **Practice:** <br>&emsp; + Launch RDS MySQL (Free Tier) <br>&emsp; + SSH into EC2 and test Database connection <br>&emsp; + Clean up resources | 02/09/2026   | 02/09/2026      | <https://cloudjourney.awsstudygroup.com/> |


### Week 4 Achievements:

* Understood the pros and cons of different database engines on AWS:
  * Amazon RDS (Relational Database)
  * Amazon DynamoDB (Non-relational Database)
  * ...

* Grasped High Availability (HA) mechanisms for Databases:
  * Multi-AZ Failover
  * Read Replicas (Scaling read capacity)

* Successfully established secure network groups strictly for databases:
  * DB Subnet Groups
  * Security Groups blocking internet access
  * ...

* Successfully deployed a complete cloud database environment, including:
  * Initializing RDS MySQL server
  * Connecting securely from the Application tier (EC2) to the Database tier (RDS) via MySQL CLI
  * ...

* Executed basic SQL queries manually on the managed cloud DB system.
* ...