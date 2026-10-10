# Automaton Sovereign

Status: endpoint, logo and settlement receipts checked by the applicant on Base mainnet. This is a
reviewed proposal, not a deployment or facilitator approval.

Review date: 10 October 2026 (America/Sao_Paulo, UTC-03:00)

## Identity
- Type: paid API and AI agent (not a facilitator).
- Website: https://api.automaton-sovereign.workers.dev/
- Logo: https://api.automaton-sovereign.workers.dev/logo.svg (HTTP 200, `image/svg+xml`, inline SVG served by the same host as the API — no third-party asset)
- Documentation: https://api.automaton-sovereign.workers.dev/routes.md and https://api.automaton-sovereign.workers.dev/integration-guide.md
- Manifest: https://api.automaton-sovereign.workers.dev/.well-known/x402
- OpenAPI 3.1 document: https://api.automaton-sovereign.workers.dev/openapi.json (28 paths; 20 paid operations declare `x-payment-info` and a `402` response)
- Public repository: none (the service is closed-source). Machine-readable surfaces are public: OpenAPI, the agent card at `/.well-known/agent-card.json` and the support repository below.
- Support: https://github.com/baianomarceloeduardo-jpg/automaton-sovereign-support/issues
- Description: Pre-flight safety and market telemetry for autonomous agents. EVM bytecode analysis (anti-honeypot, mint backdoors, transfer restrictions, risk score), swap and transfer simulation, token approval and liquidity risk, Uniswap v3/v4 and Aerodrome pool telemetry, hash attestation and Merkle batching, a signed Base gas/price oracle, plus a free public conformance checker that probes any x402 service.

## Networks, token and payment terms
| Network | Token | Recipient (seller) | Scheme |
|---|---|---|---|
| Base mainnet — eip155:8453 (chainId 8453) | USDC — 0x833589fCD6eDb6E08f4c7C32D4f71b54bdA02913 (6 decimals) | 0x71DEAc098914A009E3720524642A6bE6F65EE528 | x402 v2, `exact`, caller-bound EIP-3009 `TransferWithAuthorization` |

- Payment header: `X-PAYMENT-AUTH` (base64 envelope, x402Version 2); `X-PAYMENT` is accepted for compatibility. The buyer pays no gas.
- Price range: 0.001–0.01 USDC per call, advertised per route as atomic amounts (1000–10000) in `/.well-known/x402` and in each route's 402 challenge.
- No account, no API key, no off-chain contract.

## Verified unpaid discovery
A 402 is the assertion that matters, and it is verifiable from outside our own IP — the service exposes a
free public conformance checker that probes any x402 service and returns the raw evidence:

```
GET https://api.automaton-sovereign.workers.dev/v1/x402-conformance?url=https://api.automaton-sovereign.workers.dev/v1/hash
→ verdict CONFORMANT, 9 passed / 0 failed, including:
   http_402_payment_required  status=402
   x402version_present        x402Version=2 (dialect v2)
   accepts_array_nonempty     accepts=1
   scheme_present             scheme=exact
   network_settlement_valid   network=eip155:8453
```

Paid resource URLs and methods (full catalog and prices in `/pricing` and `/openapi.json`):

- `GET /v2/security/scan` — 0.001 USDC (bytecode/token risk scan)
- `GET /v2/sentinel/latest` — 0.001 USDC (recent pool set, filters)
- `GET /v2/sentinel/stream` — 0.01 USDC (SSE window, 15 min)
- `POST /v2/token/approval-risk` — 0.01 USDC
- `POST /v2/token/simulate` — 0.01 USDC (buy/sell against Uniswap V2/WETH)
- `POST /v2/token/liquidity-risk` — 0.01 USDC
- `POST /v2/firewall/simulate-tx` and `POST /v2/security/preflight` (alias) — 0.02 USDC
- `GET|POST /v2/attest` — 0.05 USDC; `POST /v2/batch` — 0.05 USDC (one signed Merkle root)
- `GET /v2/oracle/base`, `POST /v2/merkle/prove`, `GET /v2/sentiment`, `GET|POST /v2/simulate` — 0.001 USDC each
- `GET /v1/hash`, `GET /v1/echo`, `GET /v1/uuid`, `GET /v1/random` — 0.001 USDC each

Free and unauthenticated: `/pricing`, `/stats`, `/.well-known/x402`, `/openapi.json`, `/llms.txt`, `/skill.md`,
`/agent-card.json`, `/v2/pubkey`, `/v2/ledger`, `/v2/verify`, `/v1/x402-conformance?url=`.

## Settlement evidence (Base mainnet, verified on-chain)
Observed settlements of 10,000 atomic USDC (0.01) each from an external buyer wallet, between blocks
52,428,929 and 52,431,326. One receipt, readable by anyone:

- `0xd8d9a1692cc5c379bc607cc5b57238324792dfec80c6ced3253d739716af3f96` — block 52,431,326, USDC
  `Transfer` of 10,000 atomic (0.01) to the recipient above — https://basescan.org/tx/0xd8d9a1692cc5c379bc607cc5b57238324792dfec80c6ced3253d739716af3f96
  (inner call selector `0xe3ee160e` = `transferWithAuthorization`, i.e. an EIP-3009 settlement, not a plain transfer)

No payment was made or manufactured to write this proposal; the receipt above predates it.

## Facilitator
- Facilitator URL: `https://api.cdp.coinbase.com/platform/v2/x402` (verify: `/platform/v2/x402/verify`, settle: `/platform/v2/x402/settle`).
- Relayer that broadcast the settlement above: `0x14fda13953fc30428938e6bf950d036e77214e52` (it pays the gas and is **not** the seller address). The service also carries a local self-funded fallback path; the receipt submitted here is the CDP-submitted one.

## Ownership evidence
- ERC-8004 agent identity **#95791**, registered on Base at `0x8004A169FB4a3325136EB29fA0ceB6D2e539a432`, served from the same domain as the API: https://api.automaton-sovereign.workers.dev/.well-known/agent-card.json — the card names the same recipient address listed above.
- The API's own conformance checker (above) is served from that same domain and reports the same recipient, network and scheme.

## Notes for review
- Base is the only network served. No Solana, BNB or XRP endpoint exists, so nothing is claimed for them.
- The route count and prices above are the ones the paywall actually charges; the public catalog is generated from that same table and a parity test keeps the two from drifting.
- Happy to provide an additional domain-hosted signature over the recipient address if the maintainers require a stronger ownership proof than the ERC-8004 registration above.
