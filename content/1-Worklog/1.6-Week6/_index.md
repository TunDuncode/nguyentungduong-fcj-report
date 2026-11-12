---
title: "6. Building netmon-api Lambda and querying DynamoDB"
date: 2026-09-26T09:00:00+07:00
weight: 6
draft: false
description: "Building netmon-api Lambda and querying DynamoDB"
---

# 6. Building netmon-api Lambda and querying DynamoDB

### Week 6 Objectives:

- Build a Python Lambda backend without maintaining a dedicated API server.
- Query NetworkDevices using boto3.
- Inspect IAM execution roles, CloudWatch Logs, and statusCode responses.

### Tasks to be carried out this week:

| Day | Task | Start Date | Completion Date | Reference Material |
| :--- | :--- | :--- | :--- | :--- |
| Saturday (on-site) | Create/review netmon-api with a Python runtime and DynamoDB permissions. | 26/09/2026 | 26/09/2026 | [AWS Lambda](https://docs.aws.amazon.com/lambda/latest/dg/welcome.html) |
| Sunday (independent study) | Use boto3.resource("dynamodb") and table.scan(), handling LastEvaluatedKey for pagination. | 27/09/2026 | 27/09/2026 | [Boto3 DynamoDB Table](https://boto3.amazonaws.com/v1/documentation/api/latest/reference/services/dynamodb/table/index.html) |
| Monday (independent study) | Convert Decimal values to JSON-compatible numbers and return statusCode, headers, and body. | 28/09/2026 | 28/09/2026 | [AWS Lambda](https://docs.aws.amazon.com/lambda/latest/dg/welcome.html) |
| Tuesday (independent study) | Run a Lambda test event and inspect CloudWatch Logs when data is missing. | 29/09/2026 | 29/09/2026 | [AWS Lambda](https://docs.aws.amazon.com/lambda/latest/dg/welcome.html) |

### Week 6 Achievements:

- Built the **`netmon-api` Lambda → `NetworkDevices` DynamoDB** read flow.
- Handled pagination using LastEvaluatedKey and normalized numbers for JSON output.
- Learned to diagnose permissions when Lambda returns 500 rather than blaming the frontend.

