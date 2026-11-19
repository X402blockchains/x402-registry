# AutoTasker Hub — China Social Data

Status: submitted by the project maintainer. Public endpoint, x402 manifest, MCP tools and settlement ledger were checked over direct HTTP at review time. This is a listing proposal, not a deployment or facilitator approval. No figure below is manufactured.

## Basic details
- Project name: AutoTasker Hub — China Social Data
- What does it do? (2-3 sentences): An x402-native MCP server and REST API that sells Chinese social-media and market data to AI agents per call - Weibo/Douban/Zhihu/Bilibili/Tieba hotlists, cross-platform keyword search, trend prediction, and macro market signals. Agents discover resources via /.well-known/x402, receive an HTTP 402 challenge quoting an exact USDC price, and pay on Base mainnet to a published treasury; settlement is independently verifiable through a public proof endpoint.
- Type: API (plus a remote MCP server)
- Official website: https://autotasker.highkingflower.com
- Logo URL: https://github.com/breezesamuel.png (maintainer GitHub avatar; the site does not publish a separate favicon/logo asset yet)
- Documentation or getting-started link: https://autotasker.highkingflower.com/openapi.json (MCP: https://autotasker.highkingflower.com/mcp ; discovery: https://autotasker.highkingflower.com/.well-known/x402 ; llms.txt: https://autotasker.highkingflower.com/llms.txt)
- Public support channel: partners@autotasker.highkingflower.com (published as info.contact in openapi.json)

## Networks and activity
- Networks: Base (eip155:8453) only. The unpaid x402 challenge advertises network eip155:8453.
- Public explorer or analytics link, if available: https://basescan.org/address/0xb9A9E6d9C4Ad1635aA685bba2e235A515A94773C
- App contract/program or receiving addresses, with their networks, if available: Base (eip155:8453) payTo 0xb9A9E6d9C4Ad1635aA685bba2e235A515A94773C (USDC 0x833589fCD6eDb6E08f4c7C32D4f71b54bdA02913).
- Proof that you represent the project: public repository https://github.com/breezesamuel/autotasker-hub-aevum and the production site above; this PR is opened from the maintainer's GitHub account.

## Payments - only if your product accepts payments
- Paid endpoint and HTTP method: GET https://autotasker.highkingflower.com/api/x402/hotlist (similarly GET /api/x402/search and GET /api/x402/daily_report); MCP agents call POST /mcp with {name, arguments}. An unpaid call returns HTTP 402 with an x402 v2 challenge.
- Facilitator used: PayAI (facilitator.payai.network).
- Payment scheme/version: exact, x402Version 2.
- Token contract/decimals: USDC 0x833589fCD6eDb6E08f4c7C32D4f71b54bdA02913 on Base (6 decimals).
- Successful payment transaction link for each supported network: the production settlement ledger is https://autotasker.highkingflower.com/api/x402/proof ; at review time it reports settledCount=2, totalRevenueUsd=0.100000, firstSettledAt 2026-11-19T05:19:19Z, latestSettledAt 2026-11-19T08:05:07Z, payTo the address above, and links to BaseScan for the receiving address. Individual transaction hashes are not exposed by the proof endpoint; only the aggregate ledger and the address-level explorer are published. Do not inflate these figures.
- Facilitator applicants: not applicable (project is a paid API, not a facilitator).

## Website application
- Website application reference, if you have one: none.
- Related issue or previous pull request, if any: none.

## Verified unpaid discovery (direct HTTP, GET unless noted)
- GET /.well-known/x402 -> 200 (x402 service manifest).
- GET /api/x402/hotlist -> 402 with x402 v2 challenge: scheme=exact, network=eip155:8453, price=$0.05, payTo=0xb9A9E6d9C4Ad1635aA685bba2e235A515A94773C, asset=USDC above.
- POST /mcp initialize -> 200 (protocol 2025-06-18); tools/list -> 84 tools; unpaid tools/call -> 402 with the same challenge; invalid all-zero PAYMENT-SIGNATURE -> a different error ("not a valid x402 payload"), confirming payments are actually read.

No private contact details, passwords, API keys, private keys or signed payment authorizations are included. No test, self-payment or synthetic volume is counted as revenue.
