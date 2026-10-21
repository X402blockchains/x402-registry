# Astra market data (x402)

## Basic details
- Project name: Astra market data (x402)
- What does it do? (2–3 sentences): Pay-per-call crypto market data for AI agents. Endpoints return a top-100 market snapshot, single-coin prices, a daily market brief, a token risk check, a wallet summary and a machine-readable agent brief. No signup or API key; free sample outputs under /sample/*.
- Type: API
- Official website: https://astratc.github.io
- Logo URL: https://astratc.github.io/favicon.png
- Documentation or getting-started link: https://astra-x402-data.astratc.workers.dev/ (endpoint index) and https://dev.to/astratc/pay-per-call-crypto-data-for-ai-agents-with-x402-a-working-example-2c6b
- Public support channel: https://github.com/astratc/astratc.github.io/issues

## Networks and activity
- Networks: Base
- Public explorer or analytics link, if available: https://basescan.org/address/0x1A7Dc2677391D49FB3001AD5a1aa89A573c9b865
- App contract/program or receiving addresses, with their networks, if available: 0x1A7Dc2677391D49FB3001AD5a1aa89A573c9b865 (Base, payTo)
- Proof that you represent the project: the endpoint index at https://astra-x402-data.astratc.workers.dev/ lists the same payTo address, and https://astratc.github.io links to the API.

## Payments — only if your product accepts payments
- Paid endpoint and HTTP method: GET /v1/snapshot ($0.05), GET /v1/coin ($0.01), GET /v1/brief ($0.25), GET /v2/token-risk ($1.00), GET /v2/wallet ($0.50), GET /v2/agent-brief ($1.00)
- Facilitator used: public x402 facilitator (x402.org)
- Payment scheme/version: exact, x402 v1 (v2 headers in progress)
- Token contract/mint and decimals: USDC on Base, 0x833589fCD6eDb6E08f4c7C32D4f71b54bdA02913, 6 decimals
- Successful payment transaction link for each supported network: none yet (no settled API payments so far)
- Facilitator applicants: Not applicable

## Website application
- Website application reference, if you have one: none
- Related issue or previous pull request, if any: none
