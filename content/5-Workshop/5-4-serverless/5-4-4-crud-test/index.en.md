---
title: "5.4.4. Test CRUD and Data Queries"
date: 2026-11-11T00:00:00+07:00
draft: false
weight: 4
---

# 5.4.4. Test CRUD and Data Queries

## Goal

Validate CRUD operations on `NetworkDevices` using a dedicated **test item**, without changing the real EC2/device records used for the project.

## Sample test record

Use a `deviceId` beginning with `TEST-`, for example:

```json
{
  "deviceId": "TEST-SW01",
  "deviceName": "Switch test NetMon",
  "deviceType": "Switch",
  "ipAddress": "10.0.0.250",
  "status": "Online"
}
```

## CRUD scenario

1. **POST `/devices`**: create `TEST-SW01` and verify it exists in DynamoDB.
2. **GET `/devices`**: list devices and locate the test item.

{{< netmonimg src="images/netmon-workshop/33-dynamodb-networkdevices-2-items.png" alt="Two items in NetworkDevices" caption="Figure 33 – Two items in NetworkDevices" >}}

3. **GET `/devices/TEST-SW01`**: verify device details.

4. **PUT `/devices/TEST-SW01`**: update a value and read it back.

5. **DELETE `/devices/TEST-SW01`**: remove only the test item after collecting evidence.
6. **GET `/alerts`** and **PUT `/alerts/{id}`**: inspect alert history; do not mark genuine incidents handled without a response.

{{< netmonimg src="images/netmon-workshop/37-lambda-netmon-api-get-devices-test-200.png" alt="GET /devices returned HTTP 200 and device data" caption="Figure 37 – GET /devices returned HTTP 200 and device data" >}}


## Access control

For JWT-protected API routes, supply a Cognito Access Token carrying `netmon-api/read` or `netmon-api/write`, as required. A call without a token should receive 401.

**Status:** This is an end-to-end test plan. The available screenshots do not establish that all browser-based CRUD operations have completed successfully.

---

> **Publishing note:** Do not publish original images showing email addresses, login codes, or tokens. Screenshots in this pack come from the lab and have the account header removed; review them again before going public.

[← Back to chapter](../)
