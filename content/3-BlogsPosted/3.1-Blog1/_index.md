---
title: "3.1. Building a Serverless Device Management API on AWS"
date: 2026-11-12T00:00:00+07:00
weight: 1
chapter: false
draft: false
---

## 1. Why Serverless for device management?

For our **NetMon** internship project, we needed a simple way to maintain network-device records and support create, read, update and delete (CRUD) operations. My assigned responsibilities were **AWS Lambda, Amazon API Gateway, and Amazon DynamoDB**. Since the system is an educational simulation, a Serverless backend allows us to focus on API behavior without operating a dedicated application server.

We primarily worked in **us-east-1**. The team also created EC2 and VPC resources, but those belong to the infrastructure and monitoring part of the project rather than hosting the Lambda API.

## 2. Request flow

`Browser → API Gateway (HTTP API) → Lambda netmon-api → DynamoDB NetworkDevices`

- **API Gateway** exposes HTTP routes used by the management UI.
- **Lambda (`netmon-api`)** parses requests, applies business logic and performs CRUD operations.
- **DynamoDB (`NetworkDevices`)** stores device records keyed by `deviceId`.
- **IAM roles** grant Lambda access to the appropriate resources without embedding AWS account credentials in client code.

## 3. Data model

| Attribute | Meaning |
|---|---|
| `deviceId` | Unique device identifier / primary key |
| `deviceName` | Display name |
| `deviceType` | Router, Switch, Server, and so on |
| `ipAddress` | IP address |
| `location` | Physical or logical location |
| `status` | Simulated/monitored state |
| `cpuUsage`, `memoryUsage` | Example utilization values |
| `lastUpdated` | Last recorded update |

**Important distinction:** simulated CPU/RAM fields in this table are not automatically EC2 metrics collected by CloudWatch.

## 4. API operations

| Method | Example route | Purpose |
|---|---|---|
| `GET` | `/devices` | List devices |
| `GET` | `/devices/{id}` | Retrieve details |
| `POST` | `/devices` | Create a device |
| `PUT` | `/devices/{id}` | Update a device |
| `DELETE` | `/devices/{id}` | Delete a device |

*These are illustrative route conventions; verify the actual API Gateway route configuration before publishing a live endpoint.*

One implementation detail was **DynamoDB pagination**. A single `scan()` call does not necessarily return the complete table; the code should continue while `LastEvaluatedKey` exists.

```python
import boto3

table = boto3.resource("dynamodb").Table("NetworkDevices")

def list_devices():
    devices, options = [], {}
    while True:
        result = table.scan(**options)
        devices.extend(result.get("Items", []))
        if "LastEvaluatedKey" not in result:
            break
        options["ExclusiveStartKey"] = result["LastEvaluatedKey"]
    return devices
```

This is a simplified teaching example rather than a copy of the deployed Lambda function.

## 5. Frontend integration challenges

Testing an API in the AWS Console is different from calling it through a browser. I had to examine the API stage URL, HTTP method, **CORS** headers and JSON serialization. DynamoDB numeric values returned through Boto3 can include Python `Decimal` instances, which need explicit JSON-safe conversion.

I also tested calls from a localhost HTML page instead of relying only on Postman. A complete verification requires successful API responses, appropriate error handling, and correct access rules.

## 6. Lessons learned

This part of the internship helped me understand the separation between API routing, Lambda logic and persistent storage. My main takeaways are to agree on a stable JSON contract, give each function only the permissions it requires, and distinguish a backend that works from a fully tested end-to-end system.

**Next steps:** stronger input validation, structured activity logs, suitable pagination for larger datasets, and end-to-end CRUD tests.

## 7. References

- [AWS Lambda](https://docs.aws.amazon.com/lambda/latest/dg/welcome.html)
- [DynamoDB Scan and pagination](https://docs.aws.amazon.com/boto3/latest/reference/services/dynamodb/table/scan.html)
- [Programming DynamoDB with Python](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/programming-with-python.html)

*Publication status: personal draft, not yet published on AWS Study Group.*
