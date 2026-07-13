# Fortnox (fortnox)

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
