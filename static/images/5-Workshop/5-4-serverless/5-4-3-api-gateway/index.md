---
title: "5.4.3. Build an HTTP API with Eight Routes"
date: 2026-11-11T00:00:00+07:00
draft: false
weight: 3
---

# 5.4.3. Build an HTTP API with Eight Routes

## Objective

Create an HTTP API for NetMon management actions and integrate all routes with `netmon-api` Lambda.

## AWS Console steps

1. Open **API Gateway → APIs → Create API → HTTP API**. The group's API is called `netmon-management-api`.
2. Create or verify these routes:

![API Gateway route configuration]({{< relURL "images/netmon-workshop/api-gateway-routes.webp" >}})

*Evidence: API Gateway route configuration. Captured during the NetMon lab; the AWS account header has been removed.*


| Route | Purpose |
|---|---|
| `GET /devices` | List devices |
| `POST /devices` | Create device |
| `GET /devices/{id}` | Get device details |
| `PUT /devices/{id}` | Update device |
| `DELETE /devices/{id}` | Delete device |
| `GET /alerts` | List alerts |
| `PUT /alerts/{id}` | Update alert handling status |
| `GET /metrics` | Retrieve CPU metrics (current Lambda behavior) |

3. Under **Develop → Integrations**, select the `netmon-api` **Lambda function** in `us-east-1`, payload format **2.0**, and attach it to all eight routes.

![Eight API routes connected to netmon-api]({{< relURL "images/netmon-workshop/api-gateway-integration.webp" >}})

*Evidence: Eight API routes connected to netmon-api. Captured during the NetMon lab; the AWS account header has been removed.*

4. Under **Develop → CORS**, set allowed origin `http://localhost:5500`, methods GET/POST/PUT/DELETE/OPTIONS, and headers `authorization` and `content-type`. Credentials are not required when sending JWTs in the Authorization header.

![API Gateway CORS with Origin and Headers]({{< relURL "images/netmon-workshop/api-gateway-cors.webp" >}})

*Evidence: API Gateway CORS with Origin and Headers. Captured during the NetMon lab; the AWS account header has been removed.*

5. Under **Deploy → Stages → `$default`**, confirm **Automatic deployment = Enabled**. If disabled, deploy manually.

![The API Gateway $default stage]({{< relURL "images/netmon-workshop/api-gateway-stage.webp" >}})

*Evidence: The API Gateway $default stage. Captured during the NetMon lab; the AWS account header has been removed.*


## Initial test

Once routes have JWT authorization, requesting `GET /devices` **without** an Authorization header should return `401 Unauthorized`. This verifies the authorization layer, not the full Lambda integration. Test with a valid access token to confirm the backend.

> Do not publish real access tokens, secrets, or screenshots containing personal data.

![NetMon architecture diagram]({{< relURL "images/netmon-workshop/netmon-api-flow.png" >}})

---

> **Publishing note:** Do not publish original images showing email addresses, login codes, or tokens. Screenshots in this pack come from the lab and have the account header removed; review them again before going public.

[← Back to chapter](../)
