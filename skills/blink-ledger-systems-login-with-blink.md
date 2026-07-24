---
name: blink-login-with-blink
description: Integrate "Login with Blink" — obtain a Blink authorization code in the browser and exchange it server-side for the reader's profile. Use when adding Blink as an identity provider to a publisher site.
api: Blink Server-Side API
generated: '2026-07-20'
method: generated
source: https://docs.blink.net/docs/guides/login-with-blink.html
operations:
  - getAuthToken
  - registerOAuthApplication
  - getOAuthApplications
  - getUserProfile
sdk_operations:
  - blinkSDK.init
  - blinkSDK.getAuthorizationCode
  - blinkSDK.isAuthenticated
  - blinkSDK.onAuthenticationChange
---

# Login with Blink

Blink is the identity provider; your server never sees the reader's password. The flow is a browser-side code grab followed by a server-side exchange.

## Before you start

Client credentials are **not self-service**. Email `integration@blink.net` for a clientId and a set of client credentials (email + password). Use the test environment first.

| | Production | Test |
|---|---|---|
| SDK | `https://blink.net/1.0/blink-sdk.js` | `https://test.blink.net/1.0/blink-sdk.js` |
| API base | `https://api.blink.net` | `https://api.test.blink.net` |

Every server-side request must send:

```
Content-Type: application/json; charset=utf-8
x-requested-with: XMLHttpRequest
```

## Step 1 — Load and initialize the SDK (browser)

```html
<script src="https://blink.net/1.0/blink-sdk.js?clientId=YOUR_CLIENT_ID"></script>
```

The SDK is self-managed once the tag is present. `window.blinkSDK` appears when it has loaded; `blinkSDK.init({clientId: "YOUR_CLIENT_ID"})` initializes it explicitly, and no other SDK method may be called before initialization. Check readiness with `blinkSDK.isReadyForInit()` / `blinkSDK.isInitialized()`.

## Step 2 — Get an authorization code (browser)

Wire your own "Continue with Blink" button to `getAuthorizationCode`. Blink opens a login/signup modal and hands back a single-use code.

```js
blinkSDK.getAuthorizationCode(
  (response) => sendToMyServer(response.code),
  (error) => console.log("Login failed: " + error.message)  // {code, message}
);
```

Style the button with Blink's branded CSS. Post `response.code` to your own backend — never exchange it in the browser, because the exchange requires your `client_secret`.

## Step 3 — Get a server-side login token (`getAuthToken`)

```
POST {base}/users/login/
{"email": "<client credential email>", "password": "<client credential password>"}
→ 200 {"key": "<login token>"}
```

Send the result as `Authorization: Bearer <key>` on the remaining calls.

Errors: `1500` invalid email address · `1509` invalid credentials.

## Step 4 — Get your OAuth application config (`getOAuthApplications` / `registerOAuthApplication`)

Call `GET {base}/oauth/applications/` first — it returns an array of configs and **never errors**. If you already have one, reuse it.

Only register when the list is empty:

```
POST {base}/oauth/applications/register/
Authorization: Bearer <key>
{"name": "My Publication", "redirectUris": "https://mysite.com/callback https://mysite.com/alt"}
→ 200 {"clientId": "...", "clientSecret": "...", "redirectUris": "..."}
```

`redirectUris` is a **space-separated string**, not an array.

Errors: `1903` invalid redirect uri · `1905` invalid application name · `1906` name already exists · `1908` an application is already registered for this account — this is the signal to fall back to `getOAuthApplications`. There is **one application per account**, and registration is not idempotent, so never blind-retry it.

## Step 5 — Exchange the code for the profile (`getUserProfile`)

```
POST {base}/oauth/access_token/
Authorization: Bearer <key>
{
  "client_id": "...",
  "client_secret": "...",
  "code": "<authorization code from step 2>",
  "grant_type": "authorization_code",   // optional; only this value is accepted
  "redirect_uri": "https://mysite.com/callback"  // optional; must be one of your registered URIs
}
→ 200 {"user": {"email": "reader@example.com"}}
```

Errors: `1901` invalid grant type · `1902` invalid grant code (unknown, already used, or expired — restart at step 2) · `1904` invalid client credentials.

## Step 6 — Track session state

`blinkSDK.isAuthenticated()` returns the current state; `blinkSDK.onAuthenticationChange(cb)` fires when it changes. Re-render your UI from the callback rather than polling.

## Rules that apply throughout

- **Check the body, not the status code.** Blink returns HTTP 200 with an error body. Treat any response containing `code` + `message` (or a nested `error` object) as a failure.
- **No idempotency keys exist.** Nothing in this flow is safe to blind-retry; `registerOAuthApplication` especially.
- **`clientSecret` and the login token are secrets.** `getOAuthApplications` returns secrets in plaintext — never log or forward that response.
- **Only the profile email is returned.** Blink exposes no other identity attribute at this endpoint.

## See also

- `openapi/blink-ledger-systems-server-side-api-openapi.yml`
- `authentication/blink-ledger-systems-authentication.yml`
- `errors/blink-ledger-systems-problem-types.yml`
- `conventions/blink-ledger-systems-conventions.yml`
