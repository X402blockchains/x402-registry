# agent-audit

## Basic details
- Project name: agent-audit
- What does it do? (2–3 sentences): Pay-per-call, read-only checks for AI agents and x402 sellers. It audits one x402 seller origin (402 challenge on each paid route, price vs catalog, llms.txt, /.well-known/x402, openapi.json, dead links), checks up to 25 links per call, and verifies whether a quote appears on a cited page. Results are JSON; JavaScript is not executed and grades measure protocol conformance, not whether a seller is legitimate.
- Type: API
- Official website: https://agent-audit.agent-audit.workers.dev/ (hosted on Cloudflare Workers, workers.dev subdomain)
- Logo URL: https://agent-audit.agent-audit.workers.dev/favicon.svg
- Documentation or getting-started link: https://agent-audit.agent-audit.workers.dev/llms.txt (OpenAPI: https://agent-audit.agent-audit.workers.dev/openapi.json)
- Public support channel: parafield-dev@mail.grokbot.com (the contact published in the OpenAPI document)

## Networks and activity
- Networks: Base
- Public explorer or analytics link, if available: https://www.x402scan.com/ (origin registered); an operator test settlement exists (below); no customer payments yet
- App contract/program or receiving addresses, with their networks, if available: Base (eip155:8453) payee 0xa31bE3a1Ac1dde980dB8D18D32E7cd9Ab557360A
- Proof that you represent the project: see "Ownership reference" below.

## Payments — only if your product accepts payments
- Paid endpoint and HTTP method: GET /v1/audit?url= ($0.02, 20000 atomic), POST /v1/links ($0.01, 10000 atomic), GET /v1/quote-check?url=&quote= ($0.005, 5000 atomic). Free: GET /v1/preview (10 per hour per IP).
- Facilitator used: PayAI (https://facilitator.payai.network)
- Payment scheme/version: x402 v2, exact
- Token contract/mint and decimals: USDC on Base, 0x833589fCD6eDb6E08f4c7C32D4f71b54bdA02913, 6 decimals
- Successful payment transaction link for each supported network: see "Payment example" below (operator test).
- Facilitator applicants: Not applicable

## Website application
- Website application reference, if you have one: none
- Related issue or previous pull request, if any: none. page-read (proposals/page-read.md, same operator and payee) is in the same pull request.

## Payment example (operator test, owner-funded)
This was an operator test paid from the service's own wallet: payer and payee are the same address, so it is not a customer sale.
- Request: GET https://agent-audit.agent-audit.workers.dev/v1/audit?url=https://example.com (one call, no retry)
- Amount: 0.02 USDC (20000 atomic, 6 decimals) on Base mainnet (eip155:8453)
- Facilitator: PayAI (https://facilitator.payai.network). The settling sender 0xB2Bd29925CBbCEA7628279c91945Ca5B98bf371B is listed in PayAI's /supported signers.
- Transaction: https://basescan.org/tx/0x6523ef20991181a8d16b24b3b69d4d98061be84e858164b9257781fe00636e56 (block 52799988, status success; USDC Transfer 0xa31b…360A → 0xa31b…360A, 0.02 USDC)
- HTTP status: 200
- Decoded PAYMENT-RESPONSE: `{"success": true, "payer": "0xa31be3a1ac1dde980db8d18d32e7cd9ab557360a", "transaction": "0x6523ef20991181a8d16b24b3b69d4d98061be84e858164b9257781fe00636e56", "network": "eip155:8453"}`
- Resource output (fields trimmed; nothing sensitive in it): `{"service": "agent-audit", "target": "https://example.com/", "score": 84, "grade": "B", "counts": {"fail": 0, "warn": 4, "pass": 0}, "discovery": {"llmsTxt": 404, "wellKnownX402": 404, "openapi": 404}, "findings": ["llms-missing", "wellknown-missing", "openapi-missing", "no-endpoints"]}`

## Ownership reference
- Each service's llms.txt has an "Operator" section naming the GitHub account agent-audit-x402 (https://github.com/agent-audit-x402) and linking this proposal PR (https://github.com/X402blockchains/x402-registry/pull/14): https://agent-audit.agent-audit.workers.dev/llms.txt

## Buyer guide
- Exact x402 v2 flow (402 PAYMENT-REQUIRED → PAYMENT-SIGNATURE → PAYMENT-RESPONSE receipt), production facilitator URL, and what to do when payment status is uncertain: https://agent-audit.agent-audit.workers.dev/llms.txt, sections "How to pay (x402 v2, exact scheme)" and "If the payment status is uncertain".
