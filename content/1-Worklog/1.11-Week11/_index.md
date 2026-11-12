---
title: "11. Cognito sign-in, JWT, and test-frontend integration"
date: 2026-11-07T09:00:00+07:00
weight: 11
draft: false
description: "Cognito sign-in, JWT, and test-frontend integration"
---

# 11. Cognito sign-in, JWT, and test-frontend integration

### Week 11 Objectives:

- Understand User Pools, App Clients, Resource Servers, and JWT Authorizers.
- Connect sign-in with device-management APIs.
- Test the HTML/CSS/JavaScript frontend on localhost in VS Code.

### Tasks to be carried out this week:

| Day | Task | Start Date | Completion Date | Reference Material |
| :--- | :--- | :--- | :--- | :--- |
| Saturday (on-site) | Review the Cognito User Pool, netmon-web-client, and application sign-in domain. | 07/11/2026 | 07/11/2026 | [Amazon Cognito](https://docs.aws.amazon.com/cognito/latest/developerguide/what-is-amazon-cognito.html) |
| Sunday (independent study) | Study Authorization Code + PKCE, access tokens, ID tokens, and their different API roles. | 08/11/2026 | 08/11/2026 | [Cognito Authorization Code + PKCE](https://docs.aws.amazon.com/cognito/latest/developerguide/using-pkce-in-authorization-code.html) |
| Monday (independent study) | Review netmon-jwt-authorizer, read/write OAuth scopes, and protected HTTP routes. | 09/11/2026 | 09/11/2026 | [HTTP API JWT authorizer](https://docs.aws.amazon.com/apigateway/latest/developerguide/http-api-jwt-authorizer.html) |
| Tuesday (independent study) | Review localhost login, device list/detail, and alert-history screens; distinguish demo from live AWS data. | 10/11/2026 | 10/11/2026 | [HTTP API CORS](https://docs.aws.amazon.com/apigateway/latest/developerguide/http-api-cors.html) |

### Week 11 Achievements:

- Configured Cognito sign-in components and a JWT authorizer for the project.
- Prepared a localhost test UI and learned to distinguish 401/token errors from CORS or Lambda errors.
- **Do not claim all eight routes are end-to-end verified** until tested with valid access tokens and DynamoDB data.

