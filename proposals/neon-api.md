# Neon Developer API

## Basic details
- Project name: Neon Developer API
- What does it do? (2–3 sentences): SSRF-safe Web-to-Clean-Markdown and structured outbound link extraction API for AI agents and developers. Supports pay-per-call x402 v2/v1 micropayments in USDC on Base (`eip155:8453`), prepaid Base/Polygon USDC TxHash billing, and Streamable HTTP MCP. This is an API directory listing application, not a payment facilitator application.
- Type: API / MCP server
- Official website: https://neon-api.austneo.workers.dev
- Logo URL: https://raw.githubusercontent.com/austneo/neon-api/main/logo.svg
- Documentation or getting-started link: https://neon-api.austneo.workers.dev/docs
- Agent discovery & docs: https://neon-api.austneo.workers.dev/llms.txt | https://neon-api.austneo.workers.dev/skill.md | https://neon-api.austneo.workers.dev/.well-known/x402 | https://neon-api.austneo.workers.dev/openapi.json
- Public support channel: https://github.com/austneo/neon-api/issues

## Networks and activity
- Networks: Base (`eip155:8453`) for x402 and prepaid USDC; Polygon (`eip155:137`) for prepaid USDC
- Public explorer or analytics link, if available: https://neon-api.austneo.workers.dev/v1/stats
- App contract/program or receiving addresses, with their networks, if available: `0xfBF41F92592B3FF315983E41f058C21A1e8B8d48` (Base and Polygon)
- Proof that you represent the project (official website, repository or public announcement): https://github.com/austneo/neon-api

## Payments — only if your product accepts payments
- Paid endpoint and HTTP method: `GET/POST https://neon-api.austneo.workers.dev/v1/x402/extract` ($0.01 USDC), `GET/POST https://neon-api.austneo.workers.dev/v1/x402/links` ($0.005 USDC), `POST https://neon-api.austneo.workers.dev/v1/x402/extract/batch` ($0.05 USDC)
- Facilitator used: Public x402 facilitators (`https://openx402.ai`, `https://facilitator.payai.network`, `https://facilitator.unibase.com`)
- Payment scheme/version: `exact` (x402 v2 / v1 compatible)
- Token contract/mint and decimals: Base USDC `0x833589fCD6eDb6E08f4c7C32D4f71b54bdA02913` (6 decimals)
- Successful payment transaction link for each supported network: Pending first external mainnet settlement; live HTTP 402 payment challenges on Base (`eip155:8453`) are verified and active at the endpoints above (first settled Base TxHash will be appended once completed).
- Facilitator applicants: public supported/verify/settle URLs and signer/relayer addresses: Not applicable

## Website application
- Website application reference, if you have one: Not applicable
- Related issue or previous pull request, if any: None

Do not include private contact details, passwords, API keys, private keys or signed payment authorizations.
