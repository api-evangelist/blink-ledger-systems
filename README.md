# Blink Ledger Systems

<!-- API-EVANGELIST-PROVENANCE:BEGIN -->
> ### About this repository
>
> **This is not our API.** This repository is an independent, third-party profile of a company's
> **publicly available** API surface, maintained by [API Evangelist](https://apievangelist.com).
> API Evangelist does not operate, host, resell, or support this company's APIs, and is not
> affiliated with or endorsed by the company unless stated on the profile.
>
> **Where the information came from.** Everything here is assembled from material a member of the
> public can reach with a browser and no credentials — the company's own website, developer portal
> and documentation, the specifications it publishes for public use (OpenAPI, AsyncAPI, JSON Schema,
> `apis.json`, `llms.txt` and similar), its public repositories, and its public status, pricing and
> changelog pages. **Nothing here is obtained by breaching a system, defeating an access control, or
> using credentials of any kind.**
>
> **The rating is an independent assessment.** The Kin Score and Agent Readiness rating are
> independently calculated scores of a company's *public* API artifacts, produced by API Evangelist
> against a published rubric. They are not certifications, endorsements, security assessments, or
> audits, and they score published artifacts — not the quality, safety, or security of the software.
>
> **Corrections, re-scores, and removal are free.** No partnership, contract, or purchase is
> required, and you do not need to justify the request.
>
> - **Something wrong?** Open an issue on this repository, or email
>   [info@apievangelist.com](mailto:info@apievangelist.com).
> - **Published something new?** Ask for a re-score and we will re-run the rating.
> - **Want the listing taken down?** Say so and we will honor it. The profile is reduced to your
>   company name, a factual description, and a link to your own site, and the company is recorded as
>   **unrated** — never scored zero for having asked.
>
> **Response times.** Acknowledgement within **one business day**; removal or restriction within
> **two business days**; corrections and re-scores within **five business days**.
>
> **Not from the company, and here with a question?** You are welcome here — we would rather be the
> front line and point you the right way than have a good report go nowhere. What this repository
> can answer is narrow, though, so it is worth knowing who you are actually looking for:
>
> - **A question about how the API works, an account, billing, or a bug in the service** — that is
>   the company's own support, not us. We profile this API; we do not operate it and cannot see
>   your account.
> - **A bug in an open-source project we only catalog** — file it on that project's own repository.
>   This has happened with a real and correct bug report that reached us instead of the people who
>   could fix it, which helped nobody.
> - **Anything about this listing itself** — the description, the tags, the rating, a missing or
>   wrong artifact — is ours. Open an issue here.
> - **Not sure, or something general about API Evangelist or APIs.io** — open an issue on the
>   [APIs.io Inbox](https://github.com/api-search/inbox) and we will route it.
>
> **This repository contains no software, and we will never ask you to download anything.** There is
> no build, release, installer, or binary here — only text and machine-readable API descriptions, so
> there is nothing here that can be "corrupt" or need "repairing". Any issue, comment, or email
> claiming otherwise and offering a download link is not from us and is hostile. Do not follow the
> link; it is a lure. Report it to GitHub and, if you like, tell us at
> [info@apievangelist.com](mailto:info@apievangelist.com) so we can take it down.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

Blink (Blink Ledger Systems Inc.) builds online identity and payment technologies for digital publishers. A single Blink account works across publishers, giving readers one universal login and frictionless payment so they can subscribe, donate, or buy an individual article or podcast with one click, or enable autopay for small frequent purchases. Publishers integrate three products — Blink Identity, Blink Pay and Blink Donate — through one hosted JavaScript SDK that places Blink-managed panels into the page, a dashboard-configured User Journeys rules engine, four server-side JSON endpoints for OAuth2 login, and a signed webhook notification stream covering subscription, payment and donation events. Founded 2017; incorporated in the US in 2018 and surfaced in the API Evangelist network as a Polychain portfolio company.

**Areas:** Company · Infrastructure · Payments · Identity · Authentication · Publishing · Media · Subscription · Donations · Micropayments · Paywall · Webhook

## Blink Ledger Systems on APIs.io

Everything profiled for Blink Ledger Systems is published on APIs.io rather than in this repository. Start at the provider page — **[apis.io/providers/blink-ledger-systems/](https://apis.io/providers/blink-ledger-systems/)** — or go straight to one of the APIs or properties below.

### APIs (5)

- [Blink SDK for JavaScript](https://apis.io/apis/blink-ledger-systems/blink-ledger-systems-sdk/) — Browser SDK exposing window.blinkSDK. Provides Login with Blink (getAuthorizationCode), subscription entitlement checks (isSubscribed, getSubscription,…
- [Blink Notifications (Webhooks)](https://apis.io/apis/blink-ledger-systems/blink-ledger-systems-notifications/) — Outbound webhook stream delivering signed JSON notifications for subscription, payment and donation lifecycle events. Every payload is signed with ed25519…
- [Blink Ledger Systems Authentication API](https://apis.io/apis/blink-ledger-systems/blink-ledger-systems-authentication-api/) — Client account login and bearer token issuance.
- [Blink Ledger Systems OAuth Applications API](https://apis.io/apis/blink-ledger-systems/blink-ledger-systems-oauth-applications-api/) — Registration and retrieval of OAuth application credentials.
- [Blink Ledger Systems Users API](https://apis.io/apis/blink-ledger-systems/blink-ledger-systems-users-api/) — Blink user profile exchange.

### Published properties

Each property below is a page on APIs.io carrying the machine-readable artifact and what it says.

#### AsyncAPI (1)

Event-driven and webhook contracts.

- [Blink Ledger Systems Notifications Webhooks](https://apis.io/asyncapis/blink-ledger-systems/blink-ledger-systems-notifications-webhooks/)

#### MCP servers (1)

Model Context Protocol servers that expose the API to agents.

- [blink](https://apis.io/servers/blink-ledger-systems/blink/)

#### Agentic access (1)

Which operations an agent can call, which act, and which need a human in the loop.

- [Blink Ledger Systems Agentic Access](https://apis.io/agentic-access/blink-ledger-systems/blink-ledger-systems-agentic-access/)

#### JSON Schema (6)

The data models the API reads and writes.

- [AccessTokenRequest](https://apis.io/schemas/blink-ledger-systems/blink-ledger-systems-access-token-request/)
- [LoginRequest](https://apis.io/schemas/blink-ledger-systems/blink-ledger-systems-login-request/)
- [LoginToken](https://apis.io/schemas/blink-ledger-systems/blink-ledger-systems-login-token/)
- [OAuthApplicationConfig](https://apis.io/schemas/blink-ledger-systems/blink-ledger-systems-oauth-application-config/)
- [RegisterApplicationRequest](https://apis.io/schemas/blink-ledger-systems/blink-ledger-systems-register-application-request/)
- [UserProfileResponse](https://apis.io/schemas/blink-ledger-systems/blink-ledger-systems-user-profile-response/)

#### JSON-LD (1)

Linked-data contexts for the provider's vocabulary.

- [Blink Ledger Systems Context](https://apis.io/jsonld/blink-ledger-systems/blink-ledger-systems-context/)

#### Collections (3)

Postman and Open Collection request collections.

- [Blink Server-Side Authentication API](https://apis.io/collections/blink-ledger-systems/open-blink-ledger-systems-authentication-api/)
- [Blink Server-Side Authentication OAuth Applications API](https://apis.io/collections/blink-ledger-systems/open-blink-ledger-systems-oauth-applications-api/)
- [Blink Server-Side Authentication Users API](https://apis.io/collections/blink-ledger-systems/open-blink-ledger-systems-users-api/)

#### Overlays (1)

OpenAPI overlays, including conversational phrasing for each operation.

- [Blink Ledger Systems Server Side Api Overlay](https://apis.io/overlays/blink-ledger-systems/blink-ledger-systems-server-side-api-overlay/)

#### Governance rules (1)

Spectral rulesets for the provider's contracts.

- [Blink Ledger Systems API Rules](https://apis.io/rules/blink-ledger-systems/blink-ledger-systems-rules/)

#### Security (2)

Authentication, trust centre, and vulnerability disclosure.

- [Blink Ledger Systems Authentication](https://apis.io/security/blink-ledger-systems/blink-ledger-systems-authentication/)
- [Blink Ledger Systems Domain Security](https://apis.io/security/blink-ledger-systems/blink-ledger-systems-domain-security/)

## Where to find this API

Links to the company's own pages. This repository publishes no copy of their specifications — the canonical document is theirs and lives at the URLs below.

- [Website](https://blink.net)
- [Documentation](https://docs.blink.net/docs/getting-started/overview.html)
- [Getting started](https://docs.blink.net/docs/getting-started/quick-start.html)
- [API reference](https://docs.blink.net/docs/api-reference/functions.html)
- [Sign up](https://blink.net/login)
- [Support](https://docs.blink.net/docs/getting-started/support.html)
- [Blog](https://blink.net/blog/)
- [Terms of service](https://blink.net/terms)
- [Privacy policy](https://blink.net/privacy-policy)
- [Status](https://status.blink.net)

## API Evangelist rating

**Kin Score 40.1** — developing · rubric 0.24.0 · scored 2026-10-20

| Facet | Score |
|---|---|
| Discoverability | 78.6 |
| Contract quality | 34.7 |
| Contract governance | 67.3 |
| Operational transparency | 31.6 |
| Developer ergonomics | 63.7 |
| Access clarity | 0.0 |

**Agent readiness 30.8** — agent-ready

| Agent-readiness dimension | Result |
|---|---|
| Spec Presence | yes |
| Agentic Access | unknown |
| Reversibility Documented | — |
| MCP Server | — |
| Auth Clarity | bearer (partial credit) |
| Idempotency | — |
| Error Semantics | derived (partial credit) |
| OpenAPI Examples | — |
| Rate Limit Signal | — |
| Event Surface Described | yes |
| Agent Skills | derived (partial credit) |
| Well Known Catalog | yes |
| Consent Identity | — |
| Agent Card | — |
| Dry Run Mode | — |
| Delegated Identity | — |
| Protected Resource Metadata | — |
| Dynamic Client Registration | — |
| Agentic Commerce | — |

**Regulatory alignment 15.2** — Payments

The rubric is published at [github.com/api-evangelist/kin-score](https://github.com/api-evangelist/kin-score). The per-check breakdown behind these numbers — which checks were earned, partial or missed — along with score history and how this provider compares to its peers, is available at [apis.io/providers/blink-ledger-systems/](https://apis.io/providers/blink-ledger-systems/).

## How this profile is made

API Evangelist profiles a company's public API surface the way a developer would find it: the website, developer portal and documentation, the specifications it publishes, its public repositories, and its pricing, status and changelog pages. From that it derives the properties above — contracts split per API, workflows, schemas, collections, governance rules, plans and rate limits — and scores them against the published [Kin Score rubric](https://github.com/api-evangelist/kin-score).

The artifacts are published on [APIs.io](https://apis.io), not in this repository. This repository is the public record for Blink Ledger Systems: the place to say something is wrong, missing or out of date, and to ask for a re-score or a removal.

## Open an issue

- **Something about this listing** — a wrong description, a missing API, a stale artifact or a question about the rating: [open an issue on this repository](https://github.com/api-evangelist/blink-ledger-systems/issues/new).
- **A new API, or one that is not in the catalog yet** — [submit it on APIs.io](https://apis.io/add/).
- **Anything else** — [the APIs.io inbox](https://github.com/api-search/inbox/issues/new) or [info@apievangelist.com](mailto:info@apievangelist.com).
