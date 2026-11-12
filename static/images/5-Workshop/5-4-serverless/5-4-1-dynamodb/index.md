---
title: "5.4.1. Create NetworkDevices and NetworkAlerts Tables"
date: 2026-11-11T00:00:00+07:00
draft: false
weight: 1
---

# 5.4.1. Create NetworkDevices and NetworkAlerts Tables

## Objective

Design NoSQL storage for the device inventory and alert history. Reuse existing tables instead of creating duplicates.

## Create or verify tables

1. Open **DynamoDB → Tables** in `us-east-1`.
2. Create or verify **`NetworkDevices`** with String partition key `deviceId` and **On-demand** capacity.

![DynamoDB project table list]({{< relURL "images/netmon-workshop/dynamodb-tables.webp" >}})

*Evidence: DynamoDB project table list. Captured during the NetMon lab; the AWS account header has been removed.*

3. Create or verify **`NetworkAlerts`** with String partition key `eventId` and On-demand capacity.

![Items in the NetworkDevices table]({{< relURL "images/netmon-workshop/dynamodb-items.webp" >}})

*Evidence: Items in the NetworkDevices table. Captured during the NetMon lab; the AWS account header has been removed.*


![Alarm records in NetworkAlerts]({{< relURL "images/netmon-workshop/dynamodb-alerts.webp" >}})

*Evidence: Alarm records in NetworkAlerts. Captured during the NetMon lab; the AWS account header has been removed.*

4. A sort key is not needed for the current single-key design. Add indexes only after identifying a real query requirement.

### Example device record

```json
{
  "deviceId": "TEST-SW01",
  "deviceName": "Demo Switch",
  "deviceType": "Switch",
  "ipAddress": "10.0.0.10",
  "status": "Online"
}
```

For EC2, optional fields include `instanceId`, `region`, `monitoringSource`, and `vpcId`. **Do not enter InstanceId in the IP field**: the two fields identify different things.

### Alert history model

`NetworkAlerts` uses a unique `eventId`, with optional fields such as `alarmName`, `alarmType`, `alarmState`, `eventTime`, `deviceId`, `handlingStatus`, `reason`, and `isTest`.

## Verification

Use **Explore items → select table → Scan → Run** and confirm the records appear. `Scan` is reasonable for a small demonstration dataset; larger datasets should use a deliberate `Query` and index design.

> Avoid deleting the original `NetworkDevices` table while Lambda or the interface still depends on it.

---

> **Publishing note:** Do not publish original images showing email addresses, login codes, or tokens. Screenshots in this pack come from the lab and have the account header removed; review them again before going public.

[← Back to chapter](../)
