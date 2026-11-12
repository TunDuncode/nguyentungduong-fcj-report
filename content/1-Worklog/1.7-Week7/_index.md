---
title: "Week 7 Worklog"
date: 2026-06-01
weight: 7
chapter: false
pre: " <b> 1.7. </b> "
---



### Week 7 Objectives:

* Deploy a highly available and secure Static Website hosting environment.
* Integrate Amazon CloudFront Content Delivery Network (CDN) with Amazon S3 securely (Lab 4).

### Tasks to be carried out this week:
| Day | Task | Start Date | Completion Date | Reference Material |
| --- | --- | --- | --- | --- |
| 7   | - Learn about global Content Delivery Networks (CDN) <br>&emsp; + Amazon CloudFront fundamentals <br>&emsp; + Caching mechanics and Edge Locations | 19/09/2026 | 19/09/2026      | <https://cloudjourney.awsstudygroup.com/> |
| sunday   | - Study advanced CDN origin security features <br>&emsp; + Origin Access Control (OAC) <br> - Design a traffic workflow to block direct public access to object storage | 20/09/2026 | 20/09/2026      | <https://cloudjourney.awsstudygroup.com/> |
| 2   | - **Practice (Part 1):** <br>&emsp; + Create an Amazon S3 Bucket with private configurations <br>&emsp; + Enable Static Website Hosting feature <br>&emsp; + Upload static source files (HTML/CSS/JS) | 21/09/2026 | 21/09/2026      | <https://cloudjourney.awsstudygroup.com/> |
| 3   | - **Practice (Part 2):** <br>&emsp; + Create an Amazon CloudFront Distribution pointing to the S3 origin <br>&emsp; + Configure safe Origin Access Control (OAC) settings | 22/09/2026 | 22/09/2026      | <https://cloudjourney.awsstudygroup.com/> |
| 4   | - **Practice (Part 3):** <br>&emsp; + Update S3 Bucket Policy to explicitly grant access only to CloudFront OAC <br>&emsp; + Verify blocked direct access <br>&emsp; + Access the website via secure CloudFront domain | 23/09/2026 | 23/09/2026      | <https://cloudjourney.awsstudygroup.com/> |


### Week 7 Achievements:

* Mastered the operational logic and mechanisms of Content Delivery Networks:
  * Used Edge Locations to minimize latency patterns for worldwide end-users.
  * Understood data dissemination workflows from the central Origin to peripheral caches.
  * ...

* Successfully designed and implemented a production-grade Static Website Hosting layout:
  * Packaged web application resources safely inside specialized Amazon S3 environments.
  * Formulated CloudFront Distributions to securely manage external visitor routing.
  * ...

* Implemented strict security firewalls protecting backend data endpoints:
  * Configured Origin Access Control (OAC) cryptographic identity mappings.
  * Restructured S3 Bucket Policies to deny unencrypted public requests coming from the open internet.
  * ...

* Acquired system analysis capabilities to ensure web items are cached correctly and load smoothly over secure domain lines.
* ...