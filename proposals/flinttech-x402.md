# FLINTTECH x402

## Basic details
- Project name: FLINTTECH x402
- What does it do? (2–3 sentences): Pay-per-call JSON API for AI agents built on live public data. GET /leads returns construction permit leads, GET /contractor returns Minneapolis contractor permit history, and GET /audit runs a website and local-presence audit. No API key; requests use x402 v2 with USDC on Base.
- Type: API
- Official website: https://flinttech-x402.f1intt3ch.workers.dev/
- Logo URL: https://flinttech-x402.f1intt3ch.workers.dev/favicon.svg
- Documentation or getting-started link: https://flinttech-x402.f1intt3ch.workers.dev/llms.txt (OpenAPI: https://flinttech-x402.f1intt3ch.workers.dev/openapi.json, discovery: https://flinttech-x402.f1intt3ch.workers.dev/.well-known/x402)
- Public support channel: f1intt3ch@gmail.com (published in the service documentation and existing legal pages)
- Official project/operator Twitter/X profile: not established in the evidence reviewed on November 5, 2026; no profile URL is asserted. Operator confirmation remains outstanding.

## Networks and activity
- Networks: Base mainnet (eip155:8453)
- Public explorer or analytics link, if available: historical operator-test transaction below. Current customer activity and current Bazaar catalog inclusion were not established by this unpaid review.
- App contract/program or receiving addresses, with their networks, if available: Base (eip155:8453) payee 0x328c4Dbb5B9E0811835E7d8c58295857b4F7f7E5
- Proof that you represent the project: submitted by GitHub operator bdickie9; operator repository https://github.com/bdickie9/flinttech-x402. https://flinttech-x402.f1intt3ch.workers.dev/health and the unpaid challenges report the same payee. A service-hosted reference explicitly linking the service to bdickie9 was not found on the homepage or llms.txt in this review and remains outstanding; matching payee values alone are not independent ownership proof.

## Payments — only if your product accepts payments
- Paid endpoints and HTTP methods (existing prices unchanged):
  - GET /leads — $0.25 USDC. Example input: ?limit=5
  - GET /contractor — $0.15 USDC. Example input: ?name=Lucky%20Construction
  - GET /audit — $0.10 USDC. Example input: ?url=https%3A%2F%2Fexample.com
  - GET /report — $0.05 USDC. No input.
  - POST /analyze — $0.25 USDC. Content-Type: application/json; example body: {"query":"roofing permits last 30 days"}
  - GET /premium — $0.01 USDC. No input; this is a short paid welcome message, not a market-data report.
- Facilitator used: the current service's llms.txt identifies Coinbase CDP facilitator (@coinbase/x402). Source selects CDP when both configured CDP credentials are present, otherwise its configured fallback. No facilitator settings were changed or settlement attempted in this review.
- Payment scheme/version: x402 v2, exact
- Token contract/mint and decimals: USDC on Base, 0x833589fCD6eDb6E08f4c7C32D4f71b54bdA02913, 6 decimals
- Previously supplied operator-test transaction: https://basescan.org/tx/0x5230f11b912769e72ac50e31e59b006d6d098b91480f16247a73c88b398667e7
- Facilitator applicants: Not applicable

## Public availability and unpaid evidence — November 5, 2026
The former URL https://flinttech-x402.onrender.com returned HTTP 503, x-render-routing: suspend-by-user, and an HTML Service Suspended page. Its GET /health, GET /report, POST /analyze and GET /premium could not produce payment challenges.

The Workers URL above returned HTTP 200 for /health, /, /index, /favicon.svg, /llms.txt, /openapi.json and /.well-known/x402. Unpaid GET /report, POST /analyze with the example body, GET /premium, GET /leads?limit=5, GET /contractor?name=Lucky%20Construction and GET /audit?url=https%3A%2F%2Fexample.com returned HTTP 402 at 20:48:38–20:48:57 UTC. Each carried a decodable PAYMENT-REQUIRED header with x402Version 2 and a nonempty accepts array, also mirrored in the JSON body. Network, payee, asset, exact scheme and amounts matched the existing configuration. GET /analyze returned HTTP 405 with Allow: POST.

These observations establish an unpaid challenge response at the check times. They do not establish paid delivery, settlement success or continuous availability. The service's own /status returned a degraded status due to a timeout on free /leads/preview and reported 46 healthy runs out of 48 over its 24-hour window; that is service-reported monitoring, not independent uptime verification.

### Reproducible unpaid requests
```sh
curl -i --max-time 25 'https://flinttech-x402.f1intt3ch.workers.dev/report'
curl -i --max-time 25 -X POST 'https://flinttech-x402.f1intt3ch.workers.dev/analyze' \
  -H 'Content-Type: application/json' \
  --data '{"query":"roofing permits last 30 days"}'
curl -i --max-time 25 'https://flinttech-x402.f1intt3ch.workers.dev/premium'
```
No payment headers, wallet or credentials are needed to reproduce the HTTP 402 response. These commands do not pay.

## Historical payment example — operator report, evidence incomplete
The original proposal reported an owner-funded GET https://flinttech-x402.onrender.com/leads?type=Res&limit=3 for 0.25 USDC, HTTP 200, and the transaction linked above. It identified this as an operator test, not a customer sale. The complete actual successful response and matching decoded HTTP settlement receipt, or equivalent independently checkable request/payment correlation, were not located in this review. The prior output prefix is not sufficient proof of paid delivery. The historical report does not verify paid delivery from the Workers deployment. No new payment was made.

## Buyer instructions
1. Send the documented HTTP method and valid inputs without a payment header. An x402 v2 HTTP 402 carries base64 JSON in PAYMENT-REQUIRED; decode it and check the resource URL, Base network, USDC token, payee and amount before approving a purchase.
2. A buyer who elects to pay can use an x402 v2 client to send the matching PaymentPayload in PAYMENT-SIGNATURE and retain the response body, HTTP status and decoded PAYMENT-RESPONSE settlement receipt. Echo the advertised extensions, including bazaar, as the service documentation requests.
3. If a signed request times out or its settlement is uncertain, do not authorize another payment just to retry. Reconcile the original transaction and any receipt, and contact f1intt3ch@gmail.com with the transaction hash, request URL/method, timestamp and error. Do not send private keys, tokens or reusable signed payment authorizations.
4. If payment settled but delivery was lost, request recovery or an error refund through that contact. The existing published policy says calls failing due to the service's error are refunded to the paying wallet when the transaction hash is emailed within 7 days; see the refund link below. Automatic recovery and idempotent paid retries were not verified in this review.

## Website application
- Website application reference, if you have one: none established in this review
- Related issue or previous pull request: https://github.com/X402blockchains/x402-registry/pull/32
- Remaining review evidence: complete retained operator-test delivery/settlement correlation, service-hosted GitHub ownership reference, and confirmation of official Twitter/X profile or absence. No additional payment is proposed.

## Legal
- Terms: https://flinttech-store.pages.dev/terms/ · Privacy: https://flinttech-store.pages.dev/privacy/ · Refunds: https://flinttech-store.pages.dev/refund/
