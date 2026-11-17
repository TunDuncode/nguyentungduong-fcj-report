---
title: "TECHNICAL SHARING | RIOT GAMES' JOURNEY TO THE CLOUD"
date: 2026-11-14T00:00:00+07:00
weight: 2
chapter: false
---

# 4.2. Riot Games' Journey to the Cloud

## 1. Program Information

- **Official name:** Recap re 2024 – Riot Games' Journey to the Cloud
- **Date:** Saturday, 14/11/2026
- **Time according to the organizer's announcement:** 9:00–12:00
- **Location:** 7th Floor, Grand Terra, 36 Cat Linh, Hanoi (AWS Hanoi Office)

## 2. Introduction

On 14/11/2026, during the FCAJ Weekly Meetup, I attended the sharing session by speaker Nhan Nguyen about Riot Games' journey of moving its infrastructure to AWS. This is a topic I found quite close to what I am currently exploring: how a large system operates, when it should move to the cloud, and what moving to the cloud solves that staying on-premises does not.

## 3. Main Content

### 3.1. Challenges Before Moving to the Cloud

- Unable to run multiple games on the same infrastructure at the same time
- Each game requires its own configuration and resources, leading to waste
- Difficult to scale for seasons or events because new servers had to be purchased and installed
- Servers were fixed in one location, so players farther away experienced higher latency
- Heavy operations: patching, backup, and upgrades had to be done manually on each machine
- High fixed costs because the data center ran 24/7

### 3.2. What Moving to the Cloud Solves

- Using Amazon EKS to run multiple games on the same infrastructure, with automatic scaling based on demand
- Fast scaling: adding servers in minutes instead of weeks
- Moving databases to RDS/Aurora for faster and more stable provisioning
- Flexible costs: paying based on actual usage
- Teams can focus on games instead of struggling with infrastructure

### 3.3. What They Use to Avoid Latency

- **AWS Local Zones:** placing game matchmaking servers in major urban areas, close to players — no need to "jump" to a distant region and back
- **AWS Outposts:** AWS hardware placed in Riot's data centers in locations not yet covered by Local Zones, further reducing latency significantly
- **AWS Global Accelerator:** optimizing network routes so packets take the shortest and most stable path to the nearest server, instead of going through the normal public internet

Result: VALORANT keeps latency below 35 ms — a mandatory target to avoid "peeker's advantage" in a reflexive shooter game.

### 3.4. What Difficulties Did Riot Face When Switching Operating Systems?

Switching from Windows to Linux was not simple at all. Because the legacy C++ code had been running on Windows for 15 years, it contained a lot of "undefined behavior" — meaning the code worked on Windows in a very specific way, but when compiled and run on Linux, it produced different results.

A real example happened with the champion Gangplank:

- On Windows, Gangplank's powder kegs were processed in a fixed order, allowing players to perform a combo of placing multiple barrels and detonating them at the same time.
- When the servers switched to Linux, this processing order changed. As a result, Gangplank's multi-barrel combo no longer worked in areas that had been switched to Linux, while it still worked normally in areas still running Windows.
- The team had to trace the issue and found that the cause came from a container in the C++ standard library whose element traversal order differed between the two operating systems.

Summary: Riot Games migrated game servers from Windows to Linux to optimize operations, but still used C++. The operating system migration itself exposed hidden bugs in the legacy C++ code, causing behavior changes in the game, with Gangplank's combo as a typical example.

## 4. Relevance to the AWS NetMon Project

- **Choose a region close to users:** Riot moved servers closer to players to reduce latency — NetMon should also place EC2, CloudWatch, and Lambda in the same region close to the monitoring location.
- **CloudWatch as the center:** configure Alarms + SNS with the right thresholds and permissions to avoid false alarms or missed incidents.
- **Choose services based on the problem:** a small-scale NetMon only needs Lambda + API Gateway + DynamoDB; do not add unnecessary complexity.
- **Hidden costs:** pay attention to CloudWatch Logs, API Gateway invocation counts, and DynamoDB capacity — these can exceed the budget more easily than EC2 costs.
- **Test when changing environments:** Riot's migration from Windows to Linux exposed hidden bugs (the Gangplank combo broke) — when NetMon moves from local to real Lambda, all flows must be retested; do not assume "if it works here, it will work there."

After the event, I realized that choosing technology is not only about features but also requires considering performance, cost, and manageability in real operations.

## 5. Supporting Images

**Image 1:** Overall view of the Meetup on the 7th floor, Grand Terra on 14/11/2026 *(use your own photo or a photo permitted by the organizers)*.

![supporting image](/nguyentungduong-fcj-report/images/minh-chung/event2.jpg)

## 6. References

1. AWS for Games. [Riot Games on AWS – Life After Metal](https://www.linkedin.com/posts/awsgametech_riot-games-on-aws-life-after-metal-activity-7274871685172932609-7TIX).

2. Amazon Web Services. [AWS Business Transformed – Riot Games](https://www.linkedin.com/posts/amazon-web-services_aws-business-transformed-riot-games-activity-7138256673701257218-Voob).

*Note: The above content summarizes publicly available information. It does not describe personal activities without evidence, such as speaking, receiving awards, or taking photos with the speaker.*