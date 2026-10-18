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
- Public explorer or analytics link, if available: https://www.x402scan.com/ (origin registered); no paid activity yet
- App contract/program or receiving addresses, with their networks, if available: Base (eip155:8453) payee 0xa31bE3a1Ac1dde980dB8D18D32E7cd9Ab557360A
- Proof that you represent the project: the operator opened this pull request; the payee address and contact above are the ones published in the service's llms.txt and OpenAPI. The GitHub account is not yet linked from the site.

## Payments — only if your product accepts payments
- Paid endpoint and HTTP method: GET /v1/read?url= ($0.001 per page, 1000 atomic). Free: GET /v1/preview (title and first 300 characters, 10 per hour per IP).
- Facilitator used: PayAI (https://facilitator.payai.network)
- Payment scheme/version: x402 v2, exact
- Token contract/mint and decimals: USDC on Base, 0x833589fCD6eDb6E08f4c7C32D4f71b54bdA02913, 6 decimals
- Successful payment transaction link for each supported network: none yet; the service launched recently and has not had a paid call. I will add one here when it does.
- Facilitator applicants: Not applicable

## Website application
- Website application reference, if you have one: none
- Related issue or previous pull request, if any: none. agent-audit (proposals/agent-audit.md, same operator and payee) is in the same pull request.
