---
title: "5.5.3. Build a VS Code Test Page"
date: 2026-11-11T00:00:00+07:00
draft: false
weight: 3
---

# 5.5.3. Build a VS Code Test Page

## Objective

Use an HTML/CSS/JavaScript test interface in VS Code to sign in with Cognito, call the API, and verify real data without waiting for the final UI maintained by Manh Quan.

## Preparation

1. Open the prepared `NetMon-API-Test` project in VS Code, or use a frontend with an equivalent PKCE implementation.
2. Run a local server from the directory containing `index.html`:

```bash
python -m http.server 5500
```

3. Open `http://localhost:5500/` and make sure the page loads **before** starting Cognito sign-in.

{{< netmonimg src="images/netmon-workshop/48-cognito-managed-login-sign-in.png" alt="Managed-login sign-in page" caption="Figure 48 – Managed-login sign-in page" >}}


4. Enter the correct **Cognito domain**, **App Client ID**, and **API Gateway Invoke URL**. Never enter AWS Secret Keys or a Cognito client secret into browser code.
5. Use the frontend's sign-in button. After Cognito redirects to `/?code=...`, JavaScript completes the PKCE code exchange and receives an Access Token.
6. Test `GET /devices` and `GET /alerts`. If they succeed, create a `TEST-SW01` device, update its details, read it, and delete only that test record.

{{< netmonimg src="images/netmon-workshop/41-api-gateway-cors-localhost-5500.png" alt="CORS configuration for localhost:5500" caption="Figure 41 – CORS configuration for localhost:5500" >}}


## Troubleshooting

| Symptom | What to check |
|---|---|
| `ERR_CONNECTION_REFUSED` | No local server is listening on localhost:5500 |
| `401 Unauthorized` | Missing, invalid, or expired token |
| `403 Forbidden` | Access Token lacks the required route scope |
| CORS blocked | Incorrect allowed origin or headers in API Gateway |
| `500` | Lambda, DynamoDB, IAM, or CloudWatch Logs |

> Never publish a live `?code=` URL or real tokens. Before integrating the final UI, check that all eight routes return expected responses from the backend.

---

> **Publishing note:** Do not publish original images showing email addresses, login codes, or tokens. Screenshots in this pack come from the lab and have the account header removed; review them again before going public.

[← Back to chapter](../)
