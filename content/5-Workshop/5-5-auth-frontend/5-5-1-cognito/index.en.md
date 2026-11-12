---
title: "5.5.1. Create a Cognito User Pool and Web Client"
date: 2026-11-11T00:00:00+07:00
draft: false
weight: 1
---

# 5.5.1. Create a Cognito User Pool and Web Client

## Objective

Create a managed sign-in flow for NetMon administrators with Amazon Cognito rather than allowing unauthenticated browser access to the APIs.

## Steps

1. Open **Amazon Cognito → User pools**. Create a pool or select the existing one in `us-east-1`.

{{< netmonimg src="images/netmon-workshop/43-cognito-user-pool-overview.png" alt="Cognito user-pool overview" caption="Figure 43 – Cognito user-pool overview" >}}

2. Create an **App client** for a **Single-page application (SPA)** and name it `netmon-web-client`.

{{< netmonimg src="images/netmon-workshop/44-cognito-app-client-netmon-web-client.png" alt="Cognito netmon-web-client app client" caption="Figure 44 – Cognito netmon-web-client app client" >}}

3. Use **email** as the sign-in identifier, and keep self-registration disabled if only approved team members should have accounts.

4. Set **Allowed callback URLs** to `http://localhost:5500/`. If your frontend runs on another port, update the callback and CORS origin accordingly.

5. Enable **Authorization code grant** and configure a Cognito domain for Managed Login. Use **Authorization Code + PKCE** for the SPA; never embed a client secret in JavaScript.

{{< netmonimg src="images/netmon-workshop/45-cognito-resource-server-netmon-api-scopes.png" alt="Resource server netmon-api and two scopes" caption="Figure 45 – Resource server netmon-api and two scopes" >}}


{{< netmonimg src="images/netmon-workshop/46-cognito-domain-managed-login-issuer.png" alt="Cognito domain and issuer" caption="Figure 46 – Cognito domain and issuer" >}}


{{< netmonimg src="images/netmon-workshop/47-cognito-app-client-managed-login-pages-oauth-scopes.png" alt="Cognito managed-login and OAuth configuration" caption="Figure 47 – Cognito managed-login and OAuth configuration" >}}


{{< netmonimg src="images/netmon-workshop/48-cognito-managed-login-sign-in.png" alt="Managed-login sign-in page" caption="Figure 48 – Managed-login sign-in page" >}}

6. Open **User management → Users → Create user** and add an approved email account. A user created with a temporary password must change it during the first sign-in.

{{< netmonimg src="images/netmon-workshop/49-cognito-users-confirmed-enabled.png" alt="Two verified Cognito accounts" caption="Figure 49 – Two verified Cognito accounts" >}}


## Verification

After sign-in, Cognito redirects to the callback URL with `?code=...`. A local server must be listening at `localhost:5500`, and the frontend needs PKCE logic to exchange the code for tokens. `ERR_CONNECTION_REFUSED` typically means the local server is not running, not that Lambda is down.

> Authorization codes and tokens are temporary sensitive data and should not appear in published screenshots.

---

> **Publishing note:** Do not publish original images showing email addresses, login codes, or tokens. Screenshots in this pack come from the lab and have the account header removed; review them again before going public.

[← Back to chapter](../)
