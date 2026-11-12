---
title: "5.4.2. Build the netmon-api Python Lambda"
date: 2026-11-11T00:00:00+07:00
draft: false
weight: 2
---

# 5.4.2. Build the netmon-api Python Lambda

## Objective

Use a single Python Lambda named `netmon-api` to serve eight HTTP operations based on the request method and path, avoiding unnecessary duplicate functions for the class project.

## Steps

1. Open **Lambda → Functions → Create function → Author from scratch**. Name the function `netmon-api` and select a supported Python runtime.
2. Attach an **execution role** with access to both DynamoDB tables, `cloudwatch:GetMetricStatistics`, and CloudWatch Logs. Prefer resource-scoped DynamoDB permissions.

![AWS Lambda Console]({{< relURL "images/netmon-workshop/lambda-create.webp" >}})

*Evidence: AWS Lambda Console. Captured during the NetMon lab; the AWS account header has been removed.*

3. In code, read the method from `event.requestContext.http.method` and the URL from `event.rawPath` for **HTTP API payload format 2.0**.

![Configure Lambda and choose an execution role]({{< relURL "images/netmon-workshop/lambda-role.webp" >}})

*Evidence: Configure Lambda and choose an execution role. Captured during the NetMon lab; the AWS account header has been removed.*

4. Use `boto3.resource('dynamodb')`, validate incoming data, and return JSON through `statusCode`, `headers`, and `body`.
5. Click **Deploy**. Under **Test**, create a GET `/devices` event:

![Lambda tested after updating permissions]({{< relURL "images/netmon-workshop/lambda-test-ok.webp" >}})

*Evidence: Lambda tested after updating permissions. Captured during the NetMon lab; the AWS account header has been removed.*


```json
{
  "version": "2.0",
  "rawPath": "/devices",
  "requestContext": {"http": {"method": "GET", "path": "/devices"}}
}
```

6. Select **Test** and review the `statusCode` and response body. Test POST, PUT, and DELETE separately, preferably using devices whose IDs begin with `TEST-`.

## What has been verified

The team previously received `statusCode: 200` from a Lambda test event. That proves a test invocation was handled; it **does not prove that all eight routes were successfully tested end to end from a browser**.

## Common issues

- `AccessDeniedException`: the execution role lacks DynamoDB permissions.
- `KeyError` or `None`: API Gateway payload differs from the test event; inspect `rawPath`, `pathParameters`, and `requestContext`.
- `Internal server error`: check the stack trace under **Monitor → View CloudWatch logs**.

---

> **Publishing note:** Do not publish original images showing email addresses, login codes, or tokens. Screenshots in this pack come from the lab and have the account header removed; review them again before going public.

[← Back to chapter](../)
