# Project name
Manteclaw x402 API (Solana)

## Basic details
- Project name: Manteclaw x402 API (Solana)
- What does it do? (2–3 sentences): A pay-per-call crypto data API for AI agents: 199 paid endpoints covering Solana chain, token, wallet, DEX, DeFi, oracle and market data. Agents pay per call in USDC over the x402 protocol — no accounts, API keys or subscriptions. Prices are $0.01 per call (193 endpoints) and $0.02 (6 premium endpoints).
- Type: API
- Official website: https://manteclaw-x402-solana.fly.dev/catalog
- Logo URL: None yet
- Documentation or getting-started link: https://manteclaw-x402-solana.fly.dev/openapi.json
- Public support channel: https://github.com/manteclaw

## Networks and activity
- Networks: Solana
- Public explorer or analytics link, if available: https://solscan.io/account/Bkd6W9THp8qKgCYcamEkYx4Rk6TTHkUnRsegMaDZXwz2
- App contract/program or receiving addresses, with their networks, if available: Receiving wallet Bkd6W9THp8qKgCYcamEkYx4Rk6TTHkUnRsegMaDZXwz2 (Solana)
- Proof that you represent the project (official website, repository or public announcement): Source repository https://github.com/manteclaw/manteclaw-x402 — this proposal is filed from the project's own GitHub account (github.com/manteclaw).

## Payments — only if your product accepts payments
- Paid endpoint and HTTP method: GET https://manteclaw-x402-solana.fly.dev/defi/gas-tracker (representative endpoint; all 199 paid GET endpoints are listed in the OpenAPI document at https://manteclaw-x402-solana.fly.dev/openapi.json)
- Facilitator used: PayAI (https://facilitator.payai.network)
- Payment scheme/version: x402 v2, scheme "exact"
- Token contract/mint and decimals: USDC EPjFWdd5AufqSSqeM2qN1xzybapC8G4wEGGkZwyTDt1v, 6 decimals
- Successful payment transaction link for each supported network: None yet — the service is live and returns valid x402 v2 payment requirements (verifiable at the endpoint above), but no third-party payment has settled to the Solana receiving wallet yet.
- Facilitator applicants: Not applicable (we are a merchant, not a facilitator)

## Website application
- Website application reference, if you have one: None yet — the /apply page form is JavaScript-rendered; this PR is the application.
- Related issue or previous pull request, if any: None
