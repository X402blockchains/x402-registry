# Project name
Manteclaw x402 API (Base)

## Basic details
- Project name: Manteclaw x402 API (Base)
- What does it do? (2–3 sentences): A pay-per-call crypto data API for AI agents: 199 paid endpoints covering on-chain analytics, DeFi, token, wallet and market data. Agents pay per call in USDC over the x402 protocol — no accounts, API keys or subscriptions. Prices are $0.01 per call (193 endpoints) and $0.02 (6 premium endpoints).
- Type: API
- Official website: https://manteclaw-x402.fly.dev/catalog
- Logo URL: None yet
- Documentation or getting-started link: https://manteclaw-x402.fly.dev/openapi.json
- Public support channel: https://github.com/manteclaw

## Networks and activity
- Networks: Base
- Public explorer or analytics link, if available: https://basescan.org/address/0xea0aad6dfa33d6ea4aec842c24d2015e3a4b3175
- App contract/program or receiving addresses, with their networks, if available: Receiving wallet 0xea0aad6dfa33d6ea4aec842c24d2015e3a4b3175 (Base)
- Proof that you represent the project (official website, repository or public announcement): Source repository https://github.com/manteclaw/manteclaw-x402 — this proposal is filed from the project's own GitHub account (github.com/manteclaw).

## Payments — only if your product accepts payments
- Paid endpoint and HTTP method: GET https://manteclaw-x402.fly.dev/defi/gas-tracker (representative endpoint; all 199 paid GET endpoints are listed in the OpenAPI document at https://manteclaw-x402.fly.dev/openapi.json)
- Facilitator used: PayAI (https://facilitator.payai.network)
- Payment scheme/version: x402 v2, scheme "exact"
- Token contract/mint and decimals: USDC 0x833589fCD6eDb6E08f4c7C32D4f71b54bdA02913, 6 decimals
- Successful payment transaction link for each supported network: 46 USDC transfers at endpoint price points ($0.01/$0.02) settled to the receiving wallet on 2026-11-21 — see the wallet's token transfers: https://basescan.org/address/0xea0aad6dfa33d6ea4aec842c24d2015e3a4b3175#tokentxns
- Facilitator applicants: Not applicable (we are a merchant, not a facilitator)

## Website application
- Website application reference, if you have one: None yet — the /apply page form is JavaScript-rendered; this PR is the application.
- Related issue or previous pull request, if any: None
