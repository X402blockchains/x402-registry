# FLINTTECH x402

## Basic details
- Project name: FLINTTECH x402
- What does it do? (2–3 sentences): Pay-per-call JSON API for AI agents built on live public data. GET /leads returns live Minneapolis construction permit leads (job value, scope, address, contractor), GET /contractor returns a contractor's permit history, and GET /audit runs a live website and local-presence audit. No API key; pay per request with x402.
- Type: API
- Official website: https://flinttech-x402.onrender.com/ (hosted on Render, onrender.com subdomain)
- Logo URL: https://flinttech-x402.onrender.com/favicon.svg
- Documentation or getting-started link: https://flinttech-x402.onrender.com/llms.txt (OpenAPI: https://flinttech-x402.onrender.com/openapi.json, discovery: https://flinttech-x402.onrender.com/.well-known/x402)
- Public support channel: f1intt3ch@gmail.com (published on the Terms/Privacy pages linked from the landing page)

## Networks and activity
- Networks: Base
- Public explorer or analytics link, if available: listed in the Coinbase CDP x402 Bazaar; operator test settlements below; no customer payments yet
- App contract/program or receiving addresses, with their networks, if available: Base (eip155:8453) payee 0x328c4Dbb5B9E0811835E7d8c58295857b4F7f7E5
- Proof that you represent the project: same payee address served in every 402 challenge and in https://flinttech-x402.onrender.com/health

## Payments — only if your product accepts payments
- Paid endpoint and HTTP method: GET /leads ($0.25), GET /contractor?name= ($0.15), GET /audit?url= ($0.10), GET /report ($0.05), POST /analyze ($0.25), GET /premium ($0.01)
- Facilitator used: Coinbase CDP facilitator
- Payment scheme/version: x402 v2, exact
- Token contract/mint and decimals: USDC on Base, 0x833589fCD6eDb6E08f4c7C32D4f71b54bdA02913, 6 decimals
- Successful payment transaction link for each supported network: https://basescan.org/tx/0x5230f11b912769e72ac50e31e59b006d6d098b91480f16247a73c88b398667e7 (operator test, owner-funded: GET /leads?type=Res&limit=3, $0.25, HTTP 200)
- Facilitator applicants: Not applicable

## Website application
- Website application reference, if you have one: none
- Related issue or previous pull request, if any: none

## Payment example (operator test, owner-funded)
This was paid from the owner's own test wallet, so it is not a customer sale.
- Request: GET https://flinttech-x402.onrender.com/leads?type=Res&limit=3 (one call)
- Amount: 0.25 USDC on Base mainnet (eip155:8453)
- Transaction: https://basescan.org/tx/0x5230f11b912769e72ac50e31e59b006d6d098b91480f16247a73c88b398667e7
- HTTP status: 200; output began {"product":"FLINTTECH Metro Permit Leads","city":"Minneapolis, MN","count":3,...}

## Legal
- Terms: https://flinttech-store.pages.dev/terms/ · Privacy: https://flinttech-store.pages.dev/privacy/ · Refunds: https://flinttech-store.pages.dev/refund/
