---
title: "3.3. Signing in with Amazon Cognito and Securing APIs with JWT"
date: 2026-11-12T00:00:00+07:00
weight: 3
chapter: false
draft: false
---

## 1. Why the NetMon application needs authentication

A device-management application should not let every visitor create, update or delete network-device records. After building the Serverless API, our group explored **Amazon Cognito** for user sign-in and **API Gateway JWT authorization** to control access to protected routes.

My goal was to require sign-in before users could access the management dashboard and the alert-history features.

## 2. Authentication flow

`User → Cognito User Pool → token → Browser UI → API Gateway JWT Authorizer → Lambda → DynamoDB`

- **Cognito User Pool** manages user identities and authentication.
- **App Client** represents the browser application.
- **Cognito managed login / Hosted UI** provides the sign-in experience.
- **API Gateway JWT Authorizer** validates the token's signature and claims, including issuer, audience/client ID, validity period and optional scopes.
- **Lambda** performs the backend operation when a protected route accepts the request.

A successful sign-in does **not** automatically mean that every API route has appropriate authorization. The routes must be configured explicitly.

## 3. Integration steps

1. Create a Cognito **User Pool**.
2. Configure an **App Client** suitable for a browser-based application.
3. Set the login domain and callback URL.
4. Test user sign-in, including any required first-login password change.
5. Configure a **JWT Authorizer** for protected HTTP API routes.
6. Send a valid token using `Authorization: Bearer ...` when calling the API.
7. Verify behavior for missing, expired or otherwise invalid tokens.

Illustrative request:

```http
GET /devices HTTP/1.1
Host: example.execute-api.us-east-1.amazonaws.com
Authorization: Bearer <valid-access-token>
```

Never publish real JWTs, passwords, Client Secrets or personal account identifiers. Public browser applications should use the appropriate OAuth flow and client configuration.

## 4. Issues encountered during testing

The main troubleshooting areas were:

- **Callback URL mismatch:** login succeeds but redirects to an unexpected page.
- **JWT configuration mismatch:** issuer or audience settings cause API rejection.
- **CORS errors:** browser restrictions may block a request even when a backend endpoint works.
- **Expired tokens:** sessions need proper handling.
- **Per-route permissions:** read-only operations and destructive operations need different access controls.

I found it useful to split testing into three checkpoints: **Cognito sign-in**, **API access with a token**, and **browser UI behavior**. This avoids changing multiple services without identifying the source of an error.

## 5. Lessons and next steps

Working with Cognito helped me distinguish **authentication** (who a user is) from **authorization** (what they may do). A login form alone is not a security boundary: the API must validate tokens and the backend must still validate inputs and enforce business rules.

**Next steps:** improve login redirects, handle expiration and logout, protect sensitive CRUD routes, and show clear error messages when users lack permission.

## 6. References

- [Amazon Cognito User Pools](https://docs.aws.amazon.com/cognito/latest/developerguide/cognito-user-pools.html)
- [JWT Authorizers for API Gateway HTTP APIs](https://docs.aws.amazon.com/apigateway/latest/developerguide/http-api-jwt-authorizer.html)

*Publication status: personal draft, not yet published on AWS Study Group.*
