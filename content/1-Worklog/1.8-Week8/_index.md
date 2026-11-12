---
title: "8. CRUD operations and a consistent device API"
date: 2026-10-10T09:00:00+07:00
weight: 8
draft: false
description: "CRUD operations and a consistent device API"
---

# 8. CRUD operations and a consistent device API

### Week 8 Objectives:

- Complete the design for adding, editing, deleting, listing, and viewing devices.
- Align HTTP methods and endpoints with the frontend.
- Separate configured routes from fully tested functionality.

### Tasks to be carried out this week:

| Day | Task | Start Date | Completion Date | Reference Material |
| :--- | :--- | :--- | :--- | :--- |
| Saturday (on-site) | Configure GET /devices, POST /devices, and GET /devices/{id}. | 10/10/2026 | 10/10/2026 | [Amazon API Gateway](https://docs.aws.amazon.com/apigateway/latest/developerguide/welcome.html) |
| Sunday (independent study) | Add PUT /devices/{id} and DELETE /devices/{id} in Lambda and API Gateway. | 11/10/2026 | 11/10/2026 | [AWS Lambda](https://docs.aws.amazon.com/lambda/latest/dg/welcome.html) |
| Monday (independent study) | Handle httpMethod or requestContext.http.method, pathParameters, and JSON body. | 12/10/2026 | 12/10/2026 | [AWS Lambda](https://docs.aws.amazon.com/lambda/latest/dg/welcome.html) |
| Tuesday (independent study) | Inspect sample records after actions and add CORS and error codes for invalid inputs. | 13/10/2026 | 13/10/2026 | [Amazon DynamoDB](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/Introduction.html) |

### Week 8 Achievements:

- Configured the device-management routes and JSON conventions for the frontend.
- Learned to verify writes in **DynamoDB Explore table items**, not only via browser messages.
- The routes still require real-token tests before claiming every CRUD flow works end to end.

