# Fortnox (fortnox)

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
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

Fortnox is a Swedish cloud accounting, ERP, and business-administration platform for small and medium-sized businesses and accounting bureaus (Sweden / Nordics). Its REST API at `https://api.fortnox.se/3/` programmatically manages accounting and financial data - invoices, customers, articles, orders, offers, vouchers, accounts, suppliers, supplier invoices, projects, and financial years. Fortnox also publishes a real duplex WebSocket event stream at `wss://ws.fortnox.se/topics-v1` that pushes minimal change notifications across domains so integrations can react to changes instead of polling.

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/fortnox/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/fortnox/refs/heads/main/apis.yml)

## Access Model (Honest Up Front)

- **This is a proprietary commercial SaaS API, not open source and not a public open-data API.** You must register a developer application in the Fortnox Developer Portal and have each end customer authorize your app.
- **Authentication is OAuth2 (Authorization Code Flow).** The end customer authorizes your integration; you exchange an Authorization-Code for an Access-Token (Bearer JWT, valid 1 hour) and a Refresh-Token (valid 45 days).
  - Authorization endpoint: `https://apps.fortnox.se/oauth-v1/auth`
  - Token endpoint: `https://apps.fortnox.se/oauth-v1/token`
- **Every REST call carries two headers:** the `Access-Token` header (the Bearer JWT) **and** the `Client-Secret` header from your Fortnox app.
- **Legacy auth is gone.** The old fixed `Access-Token` / `Client-Secret` credential pair (long-lived integration keys) was fully deprecated on **30 April 2025**; all integrations must use OAuth2.
- **Rate limit:** 300 requests/minute per access-token (enforced as a sliding window of ~25 requests per 5 seconds, per client-id + tenant). Exceeding it returns HTTP 429.
- **Marketplace economics:** Fortnox operates a developer marketplace; paid integrations are billed to the customer with a revenue-share (developer receives ~75% of the integration revenue).

## Tags

- Accounting
- ERP
- Invoicing
- Bookkeeping
- Sweden
- Nordics
- Finance
- Vouchers
- Customers
- SaaS

## Timestamps

- **Created:** 2026-07-12
- **Modified:** 2026-07-12

## APIs

### Fortnox Invoices API

Create, read, update, cancel, and list customer invoices, plus actions such as bookkeep, credit, e-mail, and print. Accounts-receivable sales invoices in a Fortnox company file.

- **Human URL:** [https://www.fortnox.se/developer/resources-rest-api/invoices/invoices](https://www.fortnox.se/developer/resources-rest-api/invoices/invoices)
- **Base URL:** `https://api.fortnox.se/3`

### Fortnox Customers API

Manage the customer register - create, retrieve, update, delete, and list customers with addresses, org/VAT numbers, terms, and default accounts used across invoices, orders, and offers.

- **Human URL:** [https://www.fortnox.se/developer/resources-rest-api/customers/customers](https://www.fortnox.se/developer/resources-rest-api/customers/customers)
- **Base URL:** `https://api.fortnox.se/3`

### Fortnox Articles API

Manage the article (product/service) register used as line items on invoices, orders, and offers - pricing, units, stock quantities, sales/purchase accounts, and VAT settings.

- **Human URL:** [https://www.fortnox.se/developer/resources-rest-api/articles/articles](https://www.fortnox.se/developer/resources-rest-api/articles/articles)
- **Base URL:** `https://api.fortnox.se/3`

### Fortnox Orders API

Create, read, update, and list sales orders, and convert an order into an invoice. Orders carry customer, article lines, delivery details, and workflow status.

- **Human URL:** [https://www.fortnox.se/developer/resources-rest-api/order/orders](https://www.fortnox.se/developer/resources-rest-api/order/orders)
- **Base URL:** `https://api.fortnox.se/3`

### Fortnox Offers API

Create, read, update, and list offers (quotations), and convert an accepted offer into an order or invoice.

- **Human URL:** [https://www.fortnox.se/developer/resources-rest-api/offer/offers](https://www.fortnox.se/developer/resources-rest-api/offer/offers)
- **Base URL:** `https://api.fortnox.se/3`

### Fortnox Bookkeeping API

Post and read accounting vouchers (double-entry journal entries) into voucher series, and manage the chart of accounts and financial years vouchers are booked against. The general-ledger core of the API.

- **Human URL:** [https://www.fortnox.se/developer/resources-rest-api/vouchers/vouchers](https://www.fortnox.se/developer/resources-rest-api/vouchers/vouchers)
- **Base URL:** `https://api.fortnox.se/3`

### Fortnox Suppliers & Supplier Invoices API

Manage the supplier register and inbound supplier invoices - create, read, update, and list suppliers, and register, bookkeep, and pay supplier invoices in the accounts-payable workflow.

- **Human URL:** [https://www.fortnox.se/developer/resources-rest-api/supplier-invoices/supplier-invoices](https://www.fortnox.se/developer/resources-rest-api/supplier-invoices/supplier-invoices)
- **Base URL:** `https://api.fortnox.se/3`

### Fortnox Projects API

Create, read, update, delete, and list projects used to tag invoices, vouchers, orders, and other records for project-based accounting and reporting.

- **Human URL:** [https://www.fortnox.se/developer/resources-rest-api/projects/projects](https://www.fortnox.se/developer/resources-rest-api/projects/projects)
- **Base URL:** `https://api.fortnox.se/3`

### Fortnox Topics WebSocket API

Duplex WebSocket stream at `wss://ws.fortnox.se/topics-v1` that pushes minimal change-notification events across domains (invoices, supplier-invoices, customers, articles, orders, offers, vouchers, projects, and more) so integrations react to changes instead of polling. Kafka-backed, at-least-once delivery, per-topic offsets, up to 14-day replay.

- **Human URL:** [https://www.fortnox.se/developer/guides-and-good-to-know/websockets](https://www.fortnox.se/developer/guides-and-good-to-know/websockets)
- **Base URL:** `wss://ws.fortnox.se/topics-v1`

## Common Properties

- [Domain Security](security/fortnox-domain-security.yml)
- [Authentication](authentication/fortnox-authentication.yml)
- [LinkedIn](https://www.linkedin.com/company/fortnox-ab)
- [Website](https://www.fortnox.se)
- [Documentation](https://www.fortnox.se/developer)
- [Plans](plans/fortnox-plans-pricing.yml)
- [Rate Limits](rate-limits/fortnox-rate-limits.yml)
- [Fin Ops](finops/fortnox-finops.yml)

## Maintainers

**FN:** Kin Lane
**Email:** kin@apievangelist.com
