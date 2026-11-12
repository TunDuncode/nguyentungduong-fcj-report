---
title: "5.5.4. Sign In with PKCE and Call Protected APIs"
date: 2026-11-11T00:00:00+07:00
draft: false
weight: 4
---

# 5.5.4. Sign In with PKCE and Call Protected APIs

## Goal

Connect an HTML/JavaScript NetMon test page to Cognito and obtain an **Access Token** through Authorization Code + PKCE.

## Configuration

1. In **Cognito → App clients → `netmon-web-client`**, verify SPA type and **Authorization code grant**.
2. Use the exact callback `http://localhost:5500/` and scopes `openid email netmon-api/read netmon-api/write`; never include a client secret in browser code.
3. Start the web server first, e.g. `python -m http.server 5500`, and ensure `http://localhost:5500/` loads.

![Cognito User Pool and App Client creation success]({{< relURL "images/netmon-workshop/cognito-success.webp" >}})

*Evidence: Cognito User Pool and App Client creation success. Captured during the NetMon lab; the AWS account header has been removed.*

4. Click **Sign in** in the NetMon API Test frontend. JavaScript creates a PKCE `code_verifier` and S256 `code_challenge`, then redirects to Cognito Managed Login.

![Localhost connection error before starting a web server]({{< relURL "images/netmon-workshop/frontend-localhost.webp" >}})

*Evidence: Localhost connection error before starting a web server. Captured during the NetMon lab; the AWS account header has been removed.*

5. Cognito redirects back with `code=...`; the frontend exchanges that one-time code at `/oauth2/token` using the matching PKCE verifier.
6. Call `GET /devices` using `Authorization: Bearer <access_token>`. Distinguish missing-token 401 from insufficient-scope 403.

## Troubleshooting

- **`ERR_CONNECTION_REFUSED`** on localhost: no server is listening or the port is incorrect. A URL containing `code` does not authenticate the application by itself.
- **`invalid_grant`**: the code is expired/used, redirect URI differs, or the PKCE verifier does not match. Start a fresh login.
- **CORS**: verify `http://localhost:5500` as allowed Origin and `authorization`, `content-type` as allowed headers.
- Never publish actual codes, tokens, or PKCE verifiers.

**Status:** The team has observed password change and a redirect to localhost; browser-based PKCE exchange and authenticated data retrieval still need separate validation.

---

> **Publishing note:** Do not publish original images showing email addresses, login codes, or tokens. Screenshots in this pack come from the lab and have the account header removed; review them again before going public.

[← Back to chapter](../)
