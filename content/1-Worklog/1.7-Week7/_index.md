---
title: "7. API Gateway, HTTP routes, and CORS"
date: 2026-10-03T09:00:00+07:00
weight: 7
draft: false
description: "API Gateway, HTTP routes, and CORS"
---

# 7. API Gateway, HTTP routes, and CORS

### Week 7 Objectives:

- Expose Lambda to the browser through an HTTP API.
- Inspect routes, integrations, stages, and the Invoke URL.
- Explain CORS failures during localhost API calls.

### Tasks to be carried out this week:

| Day | Task | Start Date | Completion Date | Reference Material |
| :--- | :--- | :--- | :--- | :--- |
| Saturday (on-site) | Configure the netmon-management-api HTTP API and integrate netmon-api Lambda. | 03/10/2026 | 03/10/2026 | [Amazon API Gateway](https://docs.aws.amazon.com/apigateway/latest/developerguide/welcome.html) |
| Sunday (independent study) | Create GET /devices and review the stage, automatic deployment, and Invoke URL. | 04/10/2026 | 04/10/2026 | [Amazon API Gateway](https://docs.aws.amazon.com/apigateway/latest/developerguide/welcome.html) |
| Monday (independent study) | Configure Access-Control-Allow-Origin, methods, and headers for localhost; review OPTIONS preflight. | 05/10/2026 | 05/10/2026 | [HTTP API CORS](https://docs.aws.amazon.com/apigateway/latest/developerguide/http-api-cors.html) |
| Tuesday (independent study) | Test the endpoint using a browser, HTML/JavaScript, or C# without depending on Postman. | 06/10/2026 | 06/10/2026 | [HTTP API CORS](https://docs.aws.amazon.com/apigateway/latest/developerguide/http-api-cors.html) |

### Week 7 Achievements:

- Connected **API Gateway → Lambda** and learned to inspect JSON responses.
- Distinguished **stage/route** errors from **CORS** or Lambda failures.
- Prepared localhost API testing in VS Code.

