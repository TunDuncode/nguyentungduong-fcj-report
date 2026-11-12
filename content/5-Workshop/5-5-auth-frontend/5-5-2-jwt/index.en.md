---
title: "5.5.2. Create a JWT Authorizer and OAuth Scopes"
date: 2026-11-11T00:00:00+07:00
draft: false
weight: 2
---

# 5.5.2. Create a JWT Authorizer and OAuth Scopes

## Objective

Require a valid access token and an appropriate scope before API Gateway allows NetMon read or write operations.

## Resource server and OAuth scopes

1. Open **Cognito → User pool → Applications → Resource servers → Create resource server**.
2. Set Name `NetMon API`, Identifier `netmon-api`, and add custom scopes `read` and `write`.
3. Under **App clients → netmon-web-client → Login pages → Edit**, allow `netmon-api/read`, `netmon-api/write`, and the necessary OpenID scopes (such as `openid` and `email`). Save changes.

## JWT Authorizer

1. Open **API Gateway → netmon-management-api → Authorization → Manage authorizers → Create**.

2. Select **JWT**, name it `netmon-jwt-authorizer`, and set Identity source `$request.header.Authorization`.

3. Set Issuer to `https://cognito-idp.us-east-1.amazonaws.com/USER_POOL_ID` (replace `USER_POOL_ID`) and Audience to the **App Client ID** of `netmon-web-client`.
4. Attach it to all eight routes and set **Authorization scopes**:

| Routes | Scope |
|---|---|
| `GET` routes (`/devices`, `/devices/{id}`, `/alerts`, `/metrics`) | `netmon-api/read` |
| `POST /devices`, `PUT /devices/{id}`, `DELETE /devices/{id}`, `PUT /alerts/{id}` | `netmon-api/write` |

## Important notes

The frontend must request these scopes during login and use the **Access Token**, not the ID Token, when calling the API. Allowing both scopes on the app client does not automatically assign distinct user roles; fine-grained user authorization requires a separate design.


---

> **Publishing note:** Do not publish original images showing email addresses, login codes, or tokens. Screenshots in this pack come from the lab and have the account header removed; review them again before going public.

## Related evidence screenshots

{{< netmonimg src="images/netmon-workshop/39-api-gateway-jwt-authorizer-read-scope.png" alt="JWT authorizer and netmon-api/read scope" caption="Figure 39 – JWT authorizer and netmon-api/read scope" >}}

{{< netmonimg src="images/netmon-workshop/45-cognito-resource-server-netmon-api-scopes.png" alt="Resource server netmon-api and two scopes" caption="Figure 45 – Resource server netmon-api and two scopes" >}}

{{< netmonimg src="images/netmon-workshop/47-cognito-app-client-managed-login-pages-oauth-scopes.png" alt="Cognito managed-login and OAuth configuration" caption="Figure 47 – Cognito managed-login and OAuth configuration" >}}

[← Back to chapter](../)
