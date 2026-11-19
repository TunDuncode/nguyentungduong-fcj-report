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

{{< netmonimg src="images/netmon-workshop/38-api-gateway-netmon-management-api-routes.png" alt="Eight API Gateway routes" caption="Figure 38 – Eight API Gateway routes" >}}

| Route | Purpose |
|---|---|
| `GET /devices` | List devices |
| `POST /devices` | Create device |
| `GET /devices/{id}` | Get device details |
| `PUT /devices/{id}` | Update device |
| `DELETE /devices/{id}` | Delete device |
| `GET /alerts` | List alerts |
| `PUT /alerts/{id}` | Update alert handling status |
| `GET /metrics` | Retrieve CPU/memory and EC2 traffic when available |

3. Under **Develop → Integrations**, select the `netmon-api` **Lambda function** in `us-east-1`, payload format **2.0**, and attach it to all eight routes.

{{< netmonimg src="images/netmon-workshop/40-api-gateway-integrations-netmon-api.png" alt="API Gateway integrated with netmon-api" caption="Figure 40 – API Gateway integrated with netmon-api" >}}

4. Under **Develop → CORS**, set allowed origin `http://localhost:5500`, methods GET/POST/PUT/DELETE/OPTIONS, and headers `authorization` and `content-type`. Credentials are not required when sending JWTs in the Authorization header.

{{< netmonimg src="images/netmon-workshop/41-api-gateway-cors-localhost-5500.png" alt="CORS configuration for localhost:5500" caption="Figure 41 – CORS configuration for localhost:5500" >}}

5. Under **Deploy → Stages → `$default`**, confirm **Automatic deployment = Enabled**. If disabled, deploy manually.

{{< netmonimg src="images/netmon-workshop/42-api-gateway-default-stage-auto-deploy.png" alt="Automatically deployed $default stage" caption="Figure 42 – Automatically deployed $default stage" >}}

## Initial test

Once routes have JWT authorization, requesting `GET /devices` **without** an Authorization header should return `401 Unauthorized`. This verifies the authorization layer, not the full Lambda integration. Test with a valid access token to confirm the backend.

> Do not publish real access tokens, secrets, or screenshots containing personal data.

## Connect the newer frontend

The eight routes above are the baseline API configuration shown in the screenshots. The monitoring UI may use `GET /metrics` to retrieve CPU, memory, and traffic. If a frontend version also uses `GET /observability` or `GET /sns/status`, verify that the route exists, integrates with the intended Lambda, and uses the read scope before enabling it. These are extensions, not verified deployments based on the eight-route configuration alone.

In DevTools → Network, check the full URL, method, status code, and JSON response. A 404 may indicate a missing route or incorrect stage; 401/403 point to authentication or scope, and 500 requires CloudWatch Logs inspection.


[← Back to chapter](../)
