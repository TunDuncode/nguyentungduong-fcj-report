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
2. Create an **App client** for a **Single-page application (SPA)** and name it `netmon-web-client`.
3. Use **email** as the sign-in identifier, and keep self-registration disabled if only approved team members should have accounts.

![Create Cognito resources for the SPA]({{< relURL "images/netmon-workshop/cognito-create.webp" >}})

*Evidence: Create Cognito resources for the SPA. Captured during the NetMon lab; the AWS account header has been removed.*

4. Set **Allowed callback URLs** to `http://localhost:5500/`. If your frontend runs on another port, update the callback and CORS origin accordingly.

![Cognito User Pool and App Client creation success]({{< relURL "images/netmon-workshop/cognito-success.webp" >}})

*Evidence: Cognito User Pool and App Client creation success. Captured during the NetMon lab; the AWS account header has been removed.*

5. Enable **Authorization code grant** and configure a Cognito domain for Managed Login. Use **Authorization Code + PKCE** for the SPA; never embed a client secret in JavaScript.
6. Open **User management → Users → Create user** and add an approved email account. A user created with a temporary password must change it during the first sign-in.

## Verification

After sign-in, Cognito redirects to the callback URL with `?code=...`. A local server must be listening at `localhost:5500`, and the frontend needs PKCE logic to exchange the code for tokens. `ERR_CONNECTION_REFUSED` typically means the local server is not running, not that Lambda is down.

> Authorization codes and tokens are temporary sensitive data and should not appear in published screenshots.

---

> **Publishing note:** Do not publish original images showing email addresses, login codes, or tokens. Screenshots in this pack come from the lab and have the account header removed; review them again before going public.

[← Back to chapter](../)
