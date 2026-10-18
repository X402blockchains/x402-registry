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
- Public explorer or analytics link, if available: https://www.x402scan.com/ (origin registered); no paid activity yet
- App contract/program or receiving addresses, with their networks, if available: Base (eip155:8453) payee 0xa31bE3a1Ac1dde980dB8D18D32E7cd9Ab557360A
- Proof that you represent the project: the operator opened this pull request; the payee address and contact above are the ones published in the service's llms.txt and OpenAPI. The GitHub account is not yet linked from the site.

## Payments — only if your product accepts payments
- Paid endpoint and HTTP method: GET /v1/audit?url= ($0.02, 20000 atomic), POST /v1/links ($0.01, 10000 atomic), GET /v1/quote-check?url=&quote= ($0.005, 5000 atomic). Free: GET /v1/preview (10 per hour per IP).
- Facilitator used: PayAI (https://facilitator.payai.network)
- Payment scheme/version: x402 v2, exact
- Token contract/mint and decimals: USDC on Base, 0x833589fCD6eDb6E08f4c7C32D4f71b54bdA02913, 6 decimals
- Successful payment transaction link for each supported network: none yet; the service launched recently and has not had a paid call. I will add one here when it does.
- Facilitator applicants: Not applicable

## Website application
- Website application reference, if you have one: none
- Related issue or previous pull request, if any: none. page-read (proposals/page-read.md, same operator and payee) is in the same pull request.
