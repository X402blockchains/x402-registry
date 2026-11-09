# AuthiChain Signal

## Basic details
- Project name: AuthiChain Signal
- What does it do? (2-3 sentences): Ranked Base launchpad tape for AI agents: last rejections, LP, and bytecode as paper market data. Unpaid GET returns HTTP 402. Idle discovery is 0.01 USDC; a live RPC-OK WATCH print is 0.05 USDC on `/api/x402/signal`. Not a broadcast order and not investment advice.
- Type: API
- Official website: https://signal.authichain.com
- Logo URL: https://signal.authichain.com/favicon.ico
- Documentation or getting-started link: https://signal.authichain.com/llms.txt (OpenAPI: https://signal.authichain.com/openapi.json, catalog: https://signal.authichain.com/.well-known/x402.json, human card: https://signal.authichain.com/offer)
- Public support channel: https://signal.authichain.com/llms.txt

## Networks and activity
- Networks: Base (eip155:8453)
- Public explorer or analytics link, if available: https://basescan.org/address/0x5db511706FB6317cd23A7655F67450c5AC6e6AA2
- App contract/program or receiving addresses, with their networks, if available: Base USDC payTo 0x5db511706FB6317cd23A7655F67450c5AC6e6AA2
- Proof that you represent the project: public origin https://signal.authichain.com, catalog https://signal.authichain.com/.well-known/x402.json, and this proposal from the operator GitHub account.

## Payments — only if your product accepts payments
- Paid endpoint and HTTP method: GET https://signal.authichain.com/api/x402/discovery ($0.01, 10000 atomic) while idle. Live WATCH: GET https://signal.authichain.com/api/x402/signal ($0.05, 50000 atomic). Optional pass: GET https://signal.authichain.com/api/x402/pass ($0.10, 100000 atomic).
- Facilitator used: PayAI (https://facilitator.payai.network) with settle fallback to xpay (https://facilitator.xpay.sh). Direct settlement also accepted via X-Payment-Tx after a confirmed Base USDC Transfer to payTo.
- Payment scheme/version: x402 v2 exact
- Token contract/mint and decimals: USDC on Base, 0x833589fCD6eDb6E08f4c7C32D4f71b54bdA02913, 6 decimals
- Successful payment transaction link for each supported network: https://basescan.org/tx/0x8e314b8398e8fc2cc45bc2a17caba09608846d12498584d785f569627e453e6b (independent discovery purchase, 0.01 USDC, payer 0x739120ade7ed878fca5bbdb806263a8258fe2360, 2026-11-08)
- Facilitator applicants: Not applicable

## Website application
- Website application reference, if you have one: none
- Related issue or previous pull request, if any: none

Affiliation: submitted by the AuthiChain Signal operator.
