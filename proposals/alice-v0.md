# ALICE V0

- **Type:** API, AI agent
- **Description:** AI agent service platform with 32 pay-per-call endpoints — LLM proxy (Claude Haiku/Sonnet/Opus), crypto analytics, security scanning, smart contract auditing, and more
- **Website (HTTPS):** https://x402.alice-v0.workers.dev
- **Logo (HTTPS):** N/A
- **Documentation:** https://x402.alice-v0.workers.dev/openapi.json
- **Public repository:** https://github.com/VZero911
- **Networks:** Base mainnet (`eip155:8453`)

## Paid Resources

| Endpoint | Method | Price (USDC) | Description |
|----------|--------|-------------|-------------|
| `/v1/chat/completions` | POST | $0.005–$0.05 | OpenAI-compatible LLM proxy (Claude Haiku/Sonnet/Opus) |
| `/api/module/crypto-price` | POST | $0.001 | Real-time cryptocurrency prices |
| `/api/module/agent-task` | POST | $0.001 | Autonomous task execution |
| `/api/module/security-scan` | POST | $0.001 | Security vulnerability scanning |
| `/api/module/analyze` | POST | $0.001 | Code and data analysis |
| `/api/module/audit-contract` | POST | $0.001 | Smart contract auditing |
| + 26 more modules | POST | $0.001 each | NLP, data, blockchain tools |

- **x402 version:** v2
- **Payment scheme:** exact
- **Token:** USDC (`0x833589fCD6eDb6E08f4c7C32D4f71b54bdA02913`, 6 decimals)
- **Seller payment address:** `0x8E0014b38f3300f922100F2973b1bC749A626841`
- **Facilitator:** Coinbase CDP (`https://api.cdp.coinbase.com/platform/v2/x402`)

## Discovery Metadata

- `GET /.well-known/x402` — x402 discovery metadata
- `GET /agent.json` — Agent discovery JSON
- `GET /openapi.json` — OpenAPI 3.1 specification
- `GET /llms.txt` — LLM crawler discovery

## Evidence

Already indexed in Coinbase CDP Bazaar with 20 validated endpoints. Self-payment settlement transactions completed on Base mainnet through CDP facilitator.

## Support

- GitHub: https://github.com/VZero911
