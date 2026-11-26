# TaxRail

## Basic details
- Project name: TaxRail
- What does it do? (2–3 sentences): Autonomous pre-execution crypto, DeFi, and corporate tax-optimization rail for AI agents across the US (IRS 1099-DA, Form 8949, HIFO/SpecID, tax-loss harvesting) and Brazil (Lei 14.754, R$35k rule, Lucro Real). It offers free simulation previews plus pay-per-call x402 v2 micro-checks ($0.005-$0.10 Base USDC) and dynamic 10%-of-verified-savings unlocks returning SpecID lots, Aave v3 / 0x / CoW / Jupiter calldata, and accounting dossiers.
- Type: API
- Official website: https://taxrail.online
- Logo URL: https://api.taxrail.online/favicon.ico
- Documentation or getting-started link: https://api.taxrail.online/llms.txt (OpenAPI: https://api.taxrail.online/openapi.json, SKILL.md: https://api.taxrail.online/SKILL.md)
- Public support channel: https://github.com/SamuelAguiar12/taxrail/issues

## Networks and activity
- Networks: Base
- Public explorer or analytics link, if available: https://www.x402scan.com/ (origin `https://api.taxrail.online` registered with 5 paid routes and 6 public routes)
- App contract/program or receiving addresses, with their networks, if available: Base (eip155:8453) payee `0x0202e70990d90325A1Dca322C91471Be774E4B6f`
- Proof that you represent the project (official website, repository or public announcement): Official repository https://github.com/SamuelAguiar12/taxrail (same maintainer account `SamuelAguiar12` opening this PR), OpenAPI contact/homepage `https://taxrail.online`, and `/.well-known/x402`.

## Payments — only if your product accepts payments
- Paid endpoint and HTTP method: `GET /api/v1/x402/pre-trade-check` ($0.01 USDC, 10000 atomic), `GET /api/v1/x402/br-35k-status` ($0.005 USDC, 5000 atomic), `GET /api/v1/x402/tlh-scan` ($0.01 USDC, 10000 atomic), `POST /api/v1/x402/optimize` ($0.10 USDC, 100000 atomic), `POST /api/v1/unlock-plan` (dynamic 10% of verified tax savings). Free: `POST /api/v1/check-tax-impact`, `POST /api/v1/borrow-vs-sell`, `POST /api/v1/classify-expense`.
- Facilitator used: Coinbase CDP (`https://api.cdp.coinbase.com/platform/v2/x402`) primary + PayAI (`https://facilitator.payai.network`) fallback
- Payment scheme/version: x402 v2, exact
- Token contract/mint and decimals: USDC on Base, `0x833589fCD6eDb6E08f4c7C32D4f71b54bdA02913`, 6 decimals
- Successful payment transaction link for each supported network: https://basescan.org/tx/0x4bfee4aedd15268d9c57670e0c3ade96c7b57bb2a5764b18c9a5002433df0d1f (Base mainnet x402 v2 EIP-3009 settlement for $0.74 USDC unlocking `plan_71f4cc20-552` on $7.38 verified tax savings)
- Facilitator applicants: Not applicable

## Website application
- Website application reference, if you have one: none
- Related issue or previous pull request, if any: Proposed entry in https://github.com/X402blockchains/awesome-x402
