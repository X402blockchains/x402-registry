# AgentKit Data

## Basic details
- Project name: AgentKit Data
- What does it do? (2–3 sentences): Pay-per-call data API settled in USDC on Base via x402 v2. Three GET endpoints: web page to clean Markdown, Solana SPL/Token-2022 mint risk check, and Solana wallet portfolio snapshot. No account or API key — unpaid requests return HTTP 402 with exact-scheme payment terms.
- Type: API
- Official website: https://x402-apis-production.up.railway.app
- Logo: Not applicable
- Documentation / getting started: https://x402-apis-production.up.railway.app/openapi.json and https://x402-apis-production.up.railway.app/.well-known/x402
- Supported networks: Base mainnet (eip155:8453), USDC
- Public support channel: GitHub halfabillion (PRs/issues on listing repos)
- Public ownership reference: Live payTo `0xd9784f8122af988E51b3183F725b0b53BCb8278A` on every 402 challenge; host under Railway project operated by the submitter.

## Payment / x402
- Paid API endpoints:
  - `GET /v1/markdown` — $0.005 USDC
  - `GET /v1/solana/token-risk` — $0.02 USDC
  - `GET /v1/solana/wallet` — $0.01 USDC
- Successful payment link / verify: unpaid calls return HTTP 402 with `PAYMENT-REQUIRED` (x402 v2). Example: `curl -sI "https://x402-apis-production.up.railway.app/v1/markdown?url=https://example.com"` → 402.
- Facilitator: PayAI (`https://facilitator.payai.network`)
- Receiving wallet (payTo): `0xd9784f8122af988E51b3183F725b0b53BCb8278A` on Base

## Activity
- Not applicable yet (new listing; settlement volume will appear after paid calls).
