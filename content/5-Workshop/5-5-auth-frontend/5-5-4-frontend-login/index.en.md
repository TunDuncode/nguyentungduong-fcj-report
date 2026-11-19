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

{{< netmonimg src="images/netmon-workshop/47-cognito-app-client-managed-login-pages-oauth-scopes.png" alt="Cognito managed-login and OAuth configuration" caption="Figure 47 – Cognito managed-login and OAuth configuration" >}}

3. Start the web server first, e.g. `python -m http.server 5500`, and ensure `http://localhost:5500/` loads.

4. Click **Sign in** in the NetMon API Test frontend. JavaScript creates a PKCE `code_verifier` and S256 `code_challenge`, then redirects to Cognito Managed Login.

{{< netmonimg src="images/netmon-workshop/48-cognito-managed-login-sign-in.png" alt="Managed-login sign-in page" caption="Figure 48 – Managed-login sign-in page" >}}

5. Cognito redirects back with `code=...`; the frontend exchanges that one-time code at `/oauth2/token` using the matching PKCE verifier.
6. Call `GET /devices` using `Authorization: Bearer <access_token>`. Distinguish missing-token 401 from insufficient-scope 403.

{{< netmonimg src="images/netmon-workshop/49-cognito-users-confirmed-enabled.png" alt="Two verified Cognito accounts" caption="Figure 49 – Two verified Cognito accounts" >}}

## Sign in to NetMon Cloud V2.5

Enter the email of a provisioned Cognito account and click **Next**.

{{< netmonimg src="images/netmon-workshop/56-cognito-sign-in-email.png" alt="Cognito email sign-in" caption="Figure 56 – Cognito email sign-in" >}}

Enter the password and click **Continue**. After successful authentication, return to the application and check API connectivity. Do not publish passwords or tokens.

{{< netmonimg src="images/netmon-workshop/57-cognito-sign-in-password.png" alt="Enter the Cognito password" caption="Figure 57 – Enter the Cognito password" >}}

## Troubleshooting

- **`ERR_CONNECTION_REFUSED`** on localhost: no server is listening or the port is incorrect. A URL containing `code` does not authenticate the application by itself.
- **`invalid_grant`**: the code is expired/used, redirect URI differs, or the PKCE verifier does not match. Start a fresh login.
- **CORS**: verify `http://localhost:5500` as allowed Origin and `authorization`, `content-type` as allowed headers.
- Never publish actual codes, tokens, or PKCE verifiers.

**Status:** The team has observed password change and a redirect to localhost; browser-based PKCE exchange and authenticated data retrieval still need separate validation.

## After sign-in

The frontend sends its access token in the Authorization header; verify the device list and metrics rather than merely seeing the dashboard. When a token expires, sign in again or use a valid refresh mechanism if supported. On sign-out, clear the application authentication state and end the Cognito session using the configured URL. Do not substitute an ID token for an access token with custom scopes.

Local demo and backend tests have reported results; live PKCE exchange and all browser-to-AWS calls still require separate validation with the current frontend build.


[← Back to chapter](../)
