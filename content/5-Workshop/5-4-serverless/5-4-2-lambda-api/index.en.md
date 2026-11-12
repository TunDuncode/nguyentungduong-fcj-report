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

{{< netmonimg src="images/netmon-workshop/34-lambda-netmon-api-code-and-api-gateway.png" alt="netmon-api Lambda and API Gateway trigger" caption="Figure 34 – netmon-api Lambda and API Gateway trigger" >}}

2. Attach an **execution role** with access to both DynamoDB tables, `cloudwatch:GetMetricStatistics`, and CloudWatch Logs. Prefer resource-scoped DynamoDB permissions.

{{< netmonimg src="images/netmon-workshop/53-lambda-netmon-api-execution-role-permissions.png" alt="Lambda netmon-api execution role" caption="Figure 53 – Lambda netmon-api execution role" >}}


{{< netmonimg src="images/netmon-workshop/54-iam-netmon-api-role-permission-policies.png" alt="IAM role permission policies" caption="Figure 54 – IAM role permission policies" >}}


{{< netmonimg src="images/netmon-workshop/55-iam-netmon-api-access-policy-json.png" alt="JSON policy granting DynamoDB and CloudWatch actions" caption="Figure 55 – JSON policy granting DynamoDB and CloudWatch actions" >}}


3. In code, read the method from `event.requestContext.http.method` and the URL from `event.rawPath` for **HTTP API payload format 2.0**.

4. Use `boto3.resource('dynamodb')`, validate incoming data, and return JSON through `statusCode`, `headers`, and `body`.
5. Click **Deploy**. Under **Test**, create a GET `/devices` event:

{{< netmonimg src="images/netmon-workshop/35-lambda-netmon-api-test-succeeded-details-collapsed.png" alt="Lambda execution result (details collapsed)" caption="Figure 35 – Lambda execution result (details collapsed)" >}}


```json
{
  "version": "2.0",
  "rawPath": "/devices",
  "requestContext": {"http": {"method": "GET", "path": "/devices"}}
}
```

6. Select **Test** and review the `statusCode` and response body. Test POST, PUT, and DELETE separately, preferably using devices whose IDs begin with `TEST-`.

{{< netmonimg src="images/netmon-workshop/36-cloudwatch-logs-netmon-api-6-streams.png" alt="netmon-api CloudWatch log streams" caption="Figure 36 – netmon-api CloudWatch log streams" >}}


{{< netmonimg src="images/netmon-workshop/37-lambda-netmon-api-get-devices-test-200.png" alt="GET /devices returned HTTP 200 and device data" caption="Figure 37 – GET /devices returned HTTP 200 and device data" >}}


## What has been verified

The team previously received `statusCode: 200` from a Lambda test event. That proves a test invocation was handled; it **does not prove that all eight routes were successfully tested end to end from a browser**.

## Common issues

- `AccessDeniedException`: the execution role lacks DynamoDB permissions.
- `KeyError` or `None`: API Gateway payload differs from the test event; inspect `rawPath`, `pathParameters`, and `requestContext`.
- `Internal server error`: check the stack trace under **Monitor → View CloudWatch logs**.

---

> **Publishing note:** Do not publish original images showing email addresses, login codes, or tokens. Screenshots in this pack come from the lab and have the account header removed; review them again before going public.

[← Back to chapter](../)
