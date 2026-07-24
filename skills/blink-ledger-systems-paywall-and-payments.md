---
name: blink-paywall-and-payments
description: Gate content with Blink — check subscription state, place donation/subscribe panels, and charge for a single article with requestPayment. Use when adding a Blink paywall, donation prompt, or per-article purchase to a publisher site.
api: Blink SDK for JavaScript
generated: '2026-07-20'
method: generated
source: https://docs.blink.net/docs/api-reference/requestPayment.html
sdk_operations:
  - blinkSDK.init
  - blinkSDK.isSubscribed
  - blinkSDK.getSubscription
  - blinkSDK.onSubscriptionChange
  - blinkSDK.requestPayment
  - blinkSDK.promptSubscriptionPopup
  - blinkSDK.showDonationModal
  - blinkSDK.promptDonationPopup
  - blinkSDK.setVariable
  - blinkSDK.addFunction
---

# Paywall, donations and per-article payments

All of this runs in the browser through `window.blinkSDK`. Blink hosts the payment forms, so card data never touches your page.

## Step 1 — Load the SDK

```html
<script src="https://blink.net/1.0/blink-sdk.js?clientId=YOUR_CLIENT_ID"></script>
```

Test environment: `https://test.blink.net/1.0/blink-sdk.js`. Test cards are published in the environments doc — `4242 4242 4242 4242` (Visa), `5555 5555 5555 4444` (Mastercard), `3782 822463 10005` (Amex) and others, all with any 3-digit CVC and any future date. Real card numbers cannot be added to a test account.

## Step 2 — Decide whether to gate

```js
if (blinkSDK.isSubscribed()) {
  // show subscriber content
} else {
  // show the paywall / subscribe button
}
```

For details rather than a boolean, `blinkSDK.getSubscription()` returns a subscription object or `null`:

```
id, userId, offerId, amount, currencyCode, createdAt, canceledAt,
nextPaymentAttempt, deliveryAddressId, blinkSignature
```

`blinkSignature` is Blink's proof the user is subscribed — use it if you need to assert entitlement server-side.

Never cache the answer for the page's lifetime. Register `blinkSDK.onSubscriptionChange(cb)`; the callback receives the subscription object, or `null` when entitlement is lost, and should re-render the gate.

## Step 3 — Offer a subscription or a donation

Imperative, from your own button:

```html
<button onclick="blinkSDK.promptSubscriptionPopup()">Subscribe</button>
<button onclick="blinkSDK.showDonationModal()">Donate</button>
```

- `promptSubscriptionPopup()` — opens the Blink subscription flow.
- `showDonationModal()` — shows a configurable branded panel with a call-to-action, then the donation form.
- `promptDonationPopup()` — the same flow without that first panel.

Each handles the unauthenticated case itself: it shows login/signup first, then transforms into the target form. Do not gate these calls behind your own auth check.

Declarative, via a User Journey configured in the dashboard, which places a Blink-managed panel into every element matching a selector:

```json
{
  "condition": "adBlockEnabled",
  "action": {
    "type": "createPG",
    "selector": ".blink-donation-placement",
    "panelType": "donation"
  }
}
```

`panelType` is one of `donation`, `subscribe`, `newsletter`, `payment`, `custom`. Add `gateType` (`cover`, `preview`, `banner`, `popup`) to gate content; omit it for a plain panel.

## Step 4 — Charge for a single article

```js
blinkSDK.requestPayment(
  {
    amount: 600000,              // 60 cents — 1 USD = 1 000 000
    currencyIsoCode: "usd",
    offerId: "984534",           // optional purchase context
    comment: {},                 // optional extra info
    merchantPublicKey: "<ed25519 public key, hex>",     // optional
    paymentInfoSignature: "<ed25519 signature, hex>"    // optional
  },
  (response) => { /* paid — hide the paywall */ },
  (error)    => { /* not paid — Blink has updated its paywall */ }
);
```

`amount` is in **precise units**, not cents. Getting this wrong overcharges by 10^6, so derive it rather than hand-writing it.

`merchantPublicKey` / `paymentInfoSignature` are an optional ed25519 proof that you authorized the price — the signature covers `amount`, `currencyIsoCode`, `offerId` and `comment`. Sign server-side; never ship the private key.

## Step 5 — Reconcile server-side

The browser callback tells your UI what to do; it is not a receipt. Settle against webhooks — `payment_created`, `payment_refunded`, and the `subscription_*` events. Verify each with the ed25519 signature over the canonicalized `event` object, or the `Blink-Echo-Token` header. Respond 200 within 10 seconds or Blink retries.

Blink publishes no delivery id or dedup key, so **key your handler off `payment.id` / `subscription.id` plus `event.type`** and make it idempotent yourself.

## Custom logic

- `blinkSDK.setVariable(key, value, scope)` — `"permanent"`, `"tab"` or `"memory"` (default). Setting a variable re-evaluates any journey whose condition depends on it, which is how you trigger a panel from your own code.
- `blinkSDK.addFunction(key, fn)` — register JS that journey conditions, journey `callback` actions and panel templates can invoke. `callFunction` swallows exceptions and returns `[ok, value]`; use `getFunction(key)(...)` if you need them to propagate.

## Money and amounts

Webhook money objects carry four representations of the same value — `amount` (string, currency units), `amountInSubunits` (integer minor units), `amountPrecise` and `amountPreciseExponent` (6 in every published example). Read `amountInSubunits` for ledger work; the amount is inclusive of Blink and processor fees.

## See also

- `components/blink-ledger-systems-components.yml`
- `sandbox/blink-ledger-systems-sandbox.yml`
- `asyncapi/blink-ledger-systems-notifications-webhooks.yml`
- `data-model/blink-ledger-systems-data-model.yml`
