# Manager.io POS Extension 

This is a first-stage, bilingual (Arabic/English) POS interface for Manager.io Cloud.

## Included
- Responsive POS screen
- Arabic/English language switch
- Camera barcode scanning using the browser BarcodeDetector API where supported
- Manual barcode entry fallback
- Product search and cart
- Customer and date fields
- ILS totals
- Cash, bank, card, and pay-later payment UI
- Manager iframe `postMessage` request helper

## Important status
This is a UI/integration starter, NOT a production-ready accounting extension yet.
The current Manager.io extension API uses an iframe and `postMessage` API. The starter attempts collection reads from:
- `/api4/inventory-items`
- `/api4/customers`
- `/api4/bank-or-cash-accounts`

These collection paths and returned data shapes must be verified against the exact API available in your Manager.io Cloud account. The official public API specs currently document single-record GETs and POST transaction schemas, but a successful test from your business is still required.

Invoice/receipt creation is intentionally disabled. Before enabling it, verify:
1. Actual inventory/customer/account list response shapes.
2. Product barcode field (standard item code vs custom field).
3. Sales invoice required fields and tax configuration.
4. Receipt `paidBy` enum value and receipt line mapping.
5. Which bank/cash account is used for cash, bank transfer, and card.
6. How invoice IDs are returned and linked to receipt lines.

Do not enable writes until these mappings are tested in a test business. This avoids duplicate or incorrect accounting entries.

## Install concept
1. Host `index.html` on an HTTPS static host (Netlify, Vercel, GitHub Pages, or your own HTTPS site).
2. In Manager.io, add an extension with source `ExternalURL`.
3. Paste the hosted URL.
4. Open the extension from Manager.io. Camera access requires HTTPS and browser permission.

## Browser support
Camera scanning uses `BarcodeDetector`, which is not available in every browser. The manual barcode field remains available as a fallback. For broader browser support, integrate a maintained ZXing-based scanner after the first connection test.

## Official references
- https://www.manager.io/extend/
- https://www.manager.io/extend/openapi/
- https://www.manager.io/openapi/post-sales-invoice.json
- https://www.manager.io/openapi/post-receipt.json
