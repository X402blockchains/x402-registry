# Grey Ridge Signals — x402 DeFi & market-data API

Type: paid API (pay-per-call); not a facilitator. This is a submitted proposal for review, not a deployment or facilitator approval.

Application: https://github.com/X402blockchains/x402-registry/issues/16
Submitted: 21 October 2026 (UTC)

## Identity
- Operator: Grey Ridge Signals Group LLC
- Type: paid API; not a facilitator.
- Official website: https://greyridgesignals.ai
- Documentation / getting-started: https://x402-data-api.sigrunner.workers.dev/llms.txt (copy-paste `@x402/fetch` paid-call recipe); OpenAPI at https://x402-data-api.sigrunner.workers.dev/openapi.json
- Logo: https://greyridgesignals.ai/favicon.svg (HTTP 200; SVG)
- Live x402 manifest: https://x402-data-api.sigrunner.workers.dev/.well-known/x402
- Measured uptime: https://x402-data-api.sigrunner.workers.dev/status — 99.94% success over 1,670 probes (2026-10-19 → 2026-10-21). 5-minute free-preview probe; a measurement, not an SLA.
- Public support channel: contact@greyridgesignals.ai
- Ownership reference: the API is operated by Grey Ridge Signals Group LLC and referenced from the official website https://greyridgesignals.ai; GitHub operator `rezearcher`.
- Description: Pay-per-call DeFi and market-data for AI agents on Base. Live resources cover on-chain reads (ETH/BTC/USD Chainlink oracle prices, gas, block number, balances, token metadata), market data (crypto spot prices, perp funding, DeFi yields, prediction-market odds), and pre-trade safety (token risk reports, token security, swap-gate). All USDC on Base, x402 version 2, scheme `exact`.

## Verified unpaid discovery
`GET https://x402-data-api.sigrunner.workers.dev/chain/eth-usd` returns HTTP 402 with x402Version 2 JSON and a payment-required challenge. The scheme is `exact`.

| Network | Token | Atomic amount for /chain/eth-usd | Payment recipient |
|---|---|---|---|
| Base mainnet — eip155:8453 | USDC — 0x833589fCD6eDb6E08f4c7C32D4f71b54bdA02913 (6 decimals) | 1000 (0.001 USDC) | 0x5765ae06a52dc7A0BB71c36A11db512c7ea9ed10 |

### Price-range correction (per review)
The review noted the application said prices start at $0.002 while `/chain/eth-usd` requests 1,000 atomic ($0.001). The accurate advertised range, aligned to the live catalogue:

Price range across the live catalogue: **0.001 USDC (1,000 atomic) to 0.05 USDC (50,000 atomic)**, USDC at 6 decimals.

| Route | Method | Price (USDC) | Atomic units |
|---|---|---|---|
| `GET /chain/eth-usd` — Base ETH/USD Chainlink oracle | GET | $0.0010 | 1,000 |
| `GET /chain/btc-usd` — Base BTC/USD Chainlink oracle | GET | $0.0010 | 1,000 |
| `GET /crypto/prices` — Multi-asset crypto spot prices | GET | $0.0010 | 1,000 |
| `GET /chain/block-number` — Base latest block number | GET | $0.0020 | 2,000 |
| `GET /chain/gas-price` — Base gas price | GET | $0.0020 | 2,000 |
| `GET /defi/yields` — DeFi yield/APY data | GET | $0.0010 | 1,000 |
| `GET /crypto/funding` — Perp funding rates | GET | $0.0040 | 4,000 |
| `GET /pm/markets` — Prediction-market odds | GET | $0.0050 | 5,000 |
| `GET /gate/swap` — Pre-trade swap safety gate | GET | $0.0080 | 8,000 |
| `GET /chain/token-report` — Token risk report | GET | $0.0100 | 10,000 |
| `GET /enrich/tech-risk` — Domain/tech risk enrichment | GET | $0.0100 | 10,000 |
| `GET /scan/mcp` — MCP server security scan | GET | $0.0500 | 50,000 |

Total live resources in manifest: **62**.

## Payments
- Paid endpoints and HTTP method: 19+ live GET routes (full list in the manifest). Representative prices above.
- Facilitator used: Coinbase CDP x402 facilitator — https://api.cdp.coinbase.com/platform/v2/x402 (production; `GET /health` reports `facilitator:"cdp"`). Fallback when CDP credentials are absent is xpay — https://facilitator.xpay.sh.
- Payment scheme / version: `exact`, x402 version 2.
- Token contract and decimals: USDC `0x833589fCD6eDb6E08f4c7C32D4f71b54bdA02913`, 6 decimals, Base mainnet (eip155:8453).
- Receiving wallet: `0x5765ae06a52dc7A0BB71c36A11db512c7ea9ed10` — merchant receiving address, not a facilitator signer/relayer.
- Successful settlement: paid settlement is live. `GET /metrics` reports 5,277 settled paid calls across the catalogue, routed through the CDP facilitator. A specific Base mainnet settlement transaction link with a decoded receipt — labelled operator test, per the review guidance — will be appended to this proposal. No transaction counts or user numbers are invented here beyond the public `/metrics` figure.

## Integration
1. Call the resource URL. On `402`, read `accepts[0]`: `scheme`, `network`, `asset`, `amount`, `payTo`, `maxTimeoutSeconds`, and `extra { name, version, decimals }` (the EIP-712 domain for USDC).
2. Build an EIP-3009 `exact` USDC transfer authorization for the quoted `amount` to `payTo` on Base; resend the request with the base64 `X-PAYMENT` header. Reference client: `@x402/fetch` — recipe at `/llms.txt`.
3. On success the API returns `200` with the JSON body and an `X-PAYMENT-RESPONSE` header carrying the settlement receipt (txHash, network, payer).
4. Timeout / retry: `maxTimeoutSeconds` is 300. All paid routes are `GET` and side-effect-free, so retry idempotently on 5xx or network error; a fresh `402` re-quotes the price.
5. Free preview: every paid route exposes `/<route>/preview` returning a real sample with no payment, for wiring and testing.

## Remaining before completed integration
- Operator to append a Base mainnet settlement transaction link + decoded receipt for a named resource and amount (operator test, labelled).
- Applicant represents the project via the official website https://greyridgesignals.ai and this GitHub account.
- No historical volume, user count or ownership signature is claimed beyond the public `/metrics` figure. Figures appear only after a reliable public feed is connected.
