---
title: "5.4.5. Device Simulation and Automated Monitoring"
date: 2026-11-11T00:00:00+07:00
draft: false
weight: 5
---

# 5.4.5. Device Simulation and Automated Monitoring

## Objective

Simulate routers, switches, and servers without measurement sources to test monitoring and alerting without purchasing physical devices. EC2 metric data still comes from CloudWatch and is excluded from random generation.

## Step 1 – Register a simulated device

In **Devices**, add a test device. Use the following sample if the API uses these fields:

```json
{
  "deviceId": "TEST-SW02",
  "deviceName": "Switch Demo",
  "deviceType": "Switch",
  "ipAddress": "10.0.0.250",
  "location": "Floor 1",
  "status": "ONLINE",
  "metricsSource": "SIMULATED"
}
```

CPU/memory may be omitted if the backend supports automatic generation. Compare the `NetworkDevices` item in DynamoDB when using real AWS. Local demo values do not establish AWS persistence.

## Step 2 – Update values periodically

Distinguish two mechanisms:

- In the local demo, JavaScript can update simulated values for a browser demonstration.
- In AWS mode, a monitor function (for example `netmon-device-monitor`) requires a periodic EventBridge Scheduler or scheduled rule. It reads simulated devices, generates 0–100% values, updates status and `lastUpdated`, then checks thresholds.

For a one-minute cycle, configure `rate(1 minute)` with the correct Lambda target and inspect invocations in CloudWatch Logs. A 60-second frontend refresh does not prove Lambda is scheduled. Adjust the interval to control costs.

The monitor needs only appropriate DynamoDB access, CloudWatch Logs, and `sns:Publish` on the topic when email is required. Keep periodic simulation separate from working CRUD logic where possible.

## Step 3 – Detect alerts

For a controlled test, set simulated CPU to 96% and its threshold to 90%; keep memory below its threshold. Expected outcome: a CPU threshold breach and an alert containing the device ID, value, threshold, timestamp, and initial handling state. If AWS notification is enabled, the monitor should persist the event in `NetworkAlerts` and publish to SNS under a deduplication policy, for example only when an incident begins.

To test disconnect behavior, set the simulated status to `OFFLINE`. This does not prove a physical device lost connectivity. Real offline detection requires heartbeat, SNMP, or an appropriate agent.

## Step 4 – Verify and handle

1. Open the alert center and inspect the test device event.
2. Handle the alert and review its history, time, and status.
3. For AWS, verify `GET /alerts`, `PUT /alerts/{id}`, DynamoDB, CloudWatch Logs and SNS email if enabled.
4. Restore normal values, check that alerts do not repeat continuously, and remove the test device if no longer needed.

## Results and limitations

The demo UI has been tested with high CPU, generated metrics, and alert handling. Backend scheduling, persistence, and automatic SNS delivery must be confirmed in the deployed AWS account. Do not label simulated data as actual measurements.

[← Back to chapter](../)
