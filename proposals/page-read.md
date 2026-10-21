# page-read

## Basic details
- Project name: page-read
- What does it do? (2–3 sentences): Turns one public web page into clean markdown or text for AI agents, with title, author, published time, canonical URL and a sha256 of the result. It makes one live fetch and extracts the main content. JavaScript is not executed, output is capped at 50,000 characters (default 10,000), and fetch failures, unsupported types and unreadable pages are returned without settling payment.
- Type: API
- Official website: https://page-read.agent-audit.workers.dev/ (hosted on Cloudflare Workers, workers.dev subdomain)
- Logo URL: https://page-read.agent-audit.workers.dev/favicon.svg
- Documentation or getting-started link: https://page-read.agent-audit.workers.dev/llms.txt (OpenAPI: https://page-read.agent-audit.workers.dev/openapi.json)
- Public support channel: parafield-dev@mail.grokbot.com (the contact published in the OpenAPI document)

## Networks and activity
- Networks: Base
- Public explorer or analytics link, if available: https://www.x402scan.com/ (origin registered); an operator test settlement exists (below); no customer payments yet
- App contract/program or receiving addresses, with their networks, if available: Base (eip155:8453) payee 0xa31bE3a1Ac1dde980dB8D18D32E7cd9Ab557360A
- Proof that you represent the project: see "Ownership reference" below.

## Payments — only if your product accepts payments
- Paid endpoint and HTTP method: GET /v1/read?url= ($0.001 per page, 1000 atomic). Free: GET /v1/preview (title and first 300 characters, 10 per hour per IP).
- Facilitator used: PayAI (https://facilitator.payai.network)
- Payment scheme/version: x402 v2, exact
- Token contract/mint and decimals: USDC on Base, 0x833589fCD6eDb6E08f4c7C32D4f71b54bdA02913, 6 decimals
- Successful payment transaction link for each supported network: see "Payment example" below (operator test).
- Facilitator applicants: Not applicable

## Website application
- Website application reference, if you have one: none
- Related issue or previous pull request, if any: none. agent-audit (proposals/agent-audit.md, same operator and payee) is in the same pull request.

## Payment example (operator test, owner-funded)
This was an operator test paid from the service's own wallet: payer and payee are the same address, so it is not a customer sale.
- Request: GET https://page-read.agent-audit.workers.dev/v1/read?url=https://example.com (one call, no retry)
- Amount: 0.001 USDC (1000 atomic, 6 decimals) on Base mainnet (eip155:8453)
- Facilitator: PayAI (https://facilitator.payai.network). The settling sender 0xB2Bd29925CBbCEA7628279c91945Ca5B98bf371B is listed in PayAI's /supported signers.
- Transaction: https://basescan.org/tx/0x1866b935bd2b7c6a128858828b33ebcb73919adc6ef5017c56a816f69d2bed7a (block 52799982, status success; USDC Transfer 0xa31b…360A → 0xa31b…360A, 0.001 USDC)
- HTTP status: 200
- Decoded PAYMENT-RESPONSE: `{"success": true, "payer": "0xa31be3a1ac1dde980db8d18d32e7cd9ab557360a", "transaction": "0x1866b935bd2b7c6a128858828b33ebcb73919adc6ef5017c56a816f69d2bed7a", "network": "eip155:8453"}`
- Resource output (fields trimmed; nothing sensitive in it): `{"url": "https://example.com", "finalUrl": "https://example.com/", "upstreamStatus": 200, "title": "Example Domain", "format": "markdown", "content": "This domain is for use in documentation examples without needing permission. This is not a service; avoid relying on it for testing and monitoring purposes.", "chars": 156, "truncated": false, "sha256": "25ddf2c883e0d1958ea971d279a7e4f0fd446724ee3db7db19dadabd4a62e484", "fetchedAt": "2026-10-19T05:55:08.427Z"}`

## Ownership reference
- Each service's llms.txt has an "Operator" section naming the GitHub account agent-audit-x402 (https://github.com/agent-audit-x402) and linking this proposal PR (https://github.com/X402blockchains/x402-registry/pull/14): https://page-read.agent-audit.workers.dev/llms.txt

## Buyer guide
- Exact x402 v2 flow (402 PAYMENT-REQUIRED → PAYMENT-SIGNATURE → PAYMENT-RESPONSE receipt), production facilitator URL, and what to do when payment status is uncertain: https://page-read.agent-audit.workers.dev/llms.txt, sections "How to pay (x402 v2, exact scheme)" and "If the payment status is uncertain".
