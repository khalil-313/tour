# Toranj Malaysia Travel — modular prototype v2

## What works

Responsive English homepage, destination cards, trip builder, sample hotel rates, guide RM160/day, private vehicle per day, optional airport transfer, cart, print-friendly **draft quotation**, and ECB MYR→EUR reference-rate endpoint. The interface never invents a live airfare. EUR is omitted when the reference feed is unavailable.

## Local setup

1. Install Node.js 20+.
2. In `server/`, run `npm install` then `npm start` (API on port 3000).
3. Serve the project root on http://localhost:5500, e.g. `npx serve -l 5500 .` or a local static server. Opening index.html directly may block JavaScript modules.
4. If your frontend uses a different origin, set `FRONTEND_ORIGIN` on the API and edit `js/config.js` as appropriate.

## Where to edit

- `index.html`: homepage, package planner and inputs.
- `css/style.css`: responsive layout, print styling.
- `js/config.js`: illustrative hotel, car and guide assumptions.
- `js/app.js`: pricing, flight search, currency and add-to-cart.
- `js/cart.js`: draft quotation / print.
- `server/index.js`: ECB reference rate, validation, API endpoints.
- `server/providers.js`: licensed flight provider integration.

## Production blockers (important)

- Hotel rates are illustrative; integrate contracted inventory and actual tax/occupancy rules.
- Obtain an authorised airline API, implement live search, baggage/fare conditions, offer expiry, reprice and booking; airline website scraping is not implemented.
- EUR uses ECB daily reference rates, NOT live transactional FX or guaranteed settlement rates. Payment provider may charge a different rate.
- The browser cart is localStorage-only and not tamperproof. On checkout, create a server-side order and revalidate all prices. Never trust totals sent by the browser.
- Connect a merchant/payment provider with hosted checkout, server-side amount verification, signed webhook, idempotency, refund handling and PCI-conscious design. Checkout remains intentionally disabled.
- Generate sequential invoices on the server **only after** verified payment/confirmed sale. Include legal company details, applicable tax fields, line items, currency, payment references and any required Malaysian e-Invoice integration. This prototype prints a draft quotation, not a tax invoice.
- Add privacy/terms/cancellation policies, customer consent, accessibility and automated tests before launch.
