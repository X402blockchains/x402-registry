# Automaton Sovereign

Status: endpoint, logo and settlement receipts checked by the applicant on Base mainnet. This is a
reviewed proposal, not a deployment or facilitator approval.

Review date: 11 October 2026 (America/Sao_Paulo, UTC-03:00)

## Identity
- Type: paid API and AI agent (not a facilitator).
- Website: https://api.automatonsvrn.xyz/
- Logo: https://api.automatonsvrn.xyz/logo.svg (HTTP 200, `image/svg+xml`, inline SVG served by the same host as the API — no third-party asset)
- Documentation: https://api.automatonsvrn.xyz/routes.md and https://api.automatonsvrn.xyz/integration-guide.md
- Manifest: https://api.automatonsvrn.xyz/.well-known/x402
- OpenAPI 3.1 document: https://api.automatonsvrn.xyz/openapi.json (28 paths; **21** paid operations declare `x-payment-info` and a `402` response, over 18 distinct paid routes — three of those routes expose `GET` and `POST`, so operation count > route count. Our earlier wording said 20: it omitted `POST /v2/security/scan`. See “Recheck, 16 October 2026” below.)
- Public repository: none (the service is closed-source). Machine-readable surfaces are public: OpenAPI, the agent card at `/.well-known/agent-card.json` and the support repository below.
- Support: https://github.com/baianomarceloeduardo-jpg/automaton-sovereign-support/issues
- Description: Pre-flight safety and market telemetry for autonomous agents. EVM bytecode analysis (anti-honeypot, mint backdoors, transfer restrictions, risk score), swap and transfer simulation, token approval and liquidity risk, Uniswap v3/v4 and Aerodrome pool telemetry, hash attestation and Merkle batching, a signed Base gas/price oracle, plus a free public conformance checker that probes any x402 service.

## Networks, token and payment terms
| Network | Token | Recipient (seller) | Scheme |
|---|---|---|---|
| Base mainnet — eip155:8453 (chainId 8453) | USDC — 0x833589fCD6eDb6E08f4c7C32D4f71b54bdA02913 (6 decimals) | 0x71DEAc098914A009E3720524642A6bE6F65EE528 | x402 v2, `exact`, caller-bound EIP-3009 `TransferWithAuthorization` |

- Payment headers: Standard x402 v2 `Payment-Signature` (case-insensitive) is supported natively; `X-PAYMENT-AUTH` (base64 envelope, x402Version 2) and `X-PAYMENT` are also accepted for backwards compatibility with existing clients.
- Settlement response: On successful payment (HTTP 200), the response includes the standard `Payment-Response` header (base64-encoded settlement metadata: tx hash, payer, recipient, amount, blockNumber) along with `X-Payment-Settled: true` and `X-Payment-Tx`.
- Authorization envelopes: Both flat payload envelopes (`{ payload: { from, to, value, validAfter, validBefore, nonce }, signature }`) and nested envelopes (`{ payload: { authorization: { ... } }, signature }`) are accepted by the server. The buyer pays no gas.
- Price range: 0.001–0.05 USDC per call, advertised per route as atomic amounts (1,000–50,000 base units) in `/.well-known/x402` `services[]`, in `/routes.md`, in `/openapi.json` and in each route's 402 challenge. The condensed `pricing[]` array currently carries the 8 featured rows and is being extended to the full 18-route table (see “Recheck, 16 October 2026”).
- Free Trial & Bypass: A free trial quota of 3 evaluation calls per day per IP is available on select routes (`/v2/security/scan` and `/v2/oracle/base`), returning HTTP 200 with headers `X-Free-Trial: true` and `X-Free-Trial-Remaining`. Clients wanting an immediate HTTP 402 challenge without consuming trial quota can pass the bypass header `X-No-Trial: 1`.
- No account, no API key, no off-chain contract.

## Verified unpaid discovery
A 402 is the assertion that matters, and it is verifiable from outside our own IP — the service exposes a
free public conformance checker that probes any x402 service and returns the raw evidence:

```
GET https://api.automatonsvrn.xyz/v1/x402-conformance?url=https://api.automatonsvrn.xyz/v1/hash
→ verdict CONFORMANT, 9 passed / 0 failed, including:
   http_402_payment_required  status=402
   x402version_present        x402Version=2 (dialect v2)
   accepts_array_nonempty     accepts=1
   scheme_present             scheme=exact
   network_settlement_valid   network=eip155:8453
```

Paid resource URLs and methods — 18 distinct paid routes / 21 HTTP operations (17 RPC service identities in
`services[]` plus the 1 SSE channel in `streams[]`; the per-route price rows are in `routes.md` and `/openapi.json`):

- `GET|POST /v2/security/scan` — 0.001 USDC (bytecode/token risk scan; both methods are paid)
- `GET /v2/sentinel/latest` — 0.001 USDC (recent pool set, filters)
- `GET /v2/sentinel/stream` — 0.01 USDC (SSE window, 15 min)
- `POST /v2/token/approval-risk` — 0.01 USDC
- `POST /v2/token/simulate` — 0.01 USDC (buy/sell against Uniswap V2/WETH)
- `POST /v2/token/liquidity-risk` — 0.01 USDC
- `POST /v2/firewall/simulate-tx` and `POST /v2/security/preflight` (alias, same handler, own 402) — 0.02 USDC
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
  (inner call selector `0xe3ee160e` = `transferWithAuthorization`, i.e. an EIP-3009 settlement, not a plain transfer).
  This receipt corresponds to a 0.01 USDC paid call against `POST /v2/token/simulate` processed via the Coinbase Developer Platform (CDP) facilitator.

No payment was made or manufactured to write this proposal; the receipt above predates it.

## Facilitator
- Facilitator URL: `https://api.cdp.coinbase.com/platform/v2/x402` (verify: `/platform/v2/x402/verify`, settle: `/platform/v2/x402/settle`).
- Relayer that broadcast the settlement above: `0x14fda13953fc30428938e6bf950d036e77214e52` (it pays the gas and is **not** the seller address). The service also carries a local self-funded fallback path; the receipt submitted here is the CDP-submitted one.

## Ownership evidence
- ERC-8004 agent identity **#95791**, registered on Base at `0x8004A169FB4a3325136EB29fA0ceB6D2e539a432`, served from the same domain as the API: https://api.automatonsvrn.xyz/.well-known/agent-card.json — the card names the same recipient address listed above.
- The API's own conformance checker (above) is served from that same domain and reports the same recipient, network and scheme.

## Notes for review
- Base is the only network served. No Solana, BNB or XRP endpoint exists, so nothing is claimed for them.
- The route count and prices above are the ones the paywall actually charges. A parity test keeps the catalog honest across `services[]`, the OpenAPI spec, `routes.md` and the edge catalog; `pricing[]` (and `paidRoutesCount`) is generated from a curated subset and is **not** yet covered by that test — see “Recheck, 16 October 2026”.
- All 5 maintainer review points (price range up to 0.05 USDC, canonical scheme `exact` with EIP-3009 authorization details, standard x402 v2 `Payment-Signature` / `Payment-Response` headers with flexible envelope support, service/operation mapping, and free trial documentation with `X-No-Trial: 1`) were addressed and deployed to live production.

## Recheck, 16 October 2026 (measurements at 14:32Z, both public hosts)

The review asked to reconcile the live counts and to explain aliases, methods and free/trial routes. Measured
values, one row per surface, with the route-by-route evidence below:

| Surface | Value | What it counts |
|---|---|---|
| `/openapi.json` | 28 paths / 31 operations / **21** carrying a `402` response and `x-payment-info` | paid **operations** |
| `/.well-known/x402` `services[]` | **17** (`kind: rpc`) | RPC **service identities** |
| `/.well-known/x402` `streams[]` | **1** (`kind: stream`) | the SSE channel |
| `serviceModel` | `{rpc: 17, streams: 1, total: 18}` | derived from the two arrays |
| `/pricing` + `/.well-known/x402` `pricing[]` | **8** | a curated subset — the defect below |
| `/health` `paidRoutesCount` and `/v1/x402/discovery` `paidRoutes[]` | **8** | same subset |
| `freeRoutes[]` | **19** | the free surface it declares (38 routes answered `200` unauthenticated when probed) |

How the numbers fit together:

- **17 → 18 service identities:** the eighteenth is the SSE channel, which lives in `streams[]` rather
  than in `services[]`. That is why the manifest's own `serviceModel` reads `17 + 1 = 18`.
- **18 → 21 operations:** 18 distinct paid routes, three of which accept two methods —
  `GET|POST /v2/security/scan`, `GET|POST /v2/simulate`, `GET|POST /v2/attest`. Our earlier wording said 20
  operations; it omitted `POST /v2/security/scan`. Each of the 21 answers `402` with the atomic amount it
  advertises (probe sweep: 41 of 42 requests across both hosts returned `402` with the expected
  `maxAmountRequired`, the exception being the intermittent window described below).
- **Aliases:** `POST /v2/security/preflight` is an alias of `POST /v2/firewall/simulate-tx` — same handler, its
  own advertised row and its own `402` at the same 0.02 USDC / 20,000 atomic units. It is a second route, not a
  second price tier.
- **Free and trial:** `freeRoutes[]` plus a 3-calls/day/IP evaluation quota on `/v2/security/scan` and
  `/v2/oracle/base` (`X-Free-Trial: true`, `X-Free-Trial-Remaining`); `X-No-Trial: 1` forces the challenge
  without consuming quota. Nothing outside those two routes is served without payment — the 0.05 USDC rows
  (`GET|POST /v2/attest`, `POST /v2/batch`, 50,000 atomic units each) were verified unpaid.

**Defect found while measuring, and it is ours:** `pricing[]`, `paidRoutesCount` and
`/v1/x402/discovery.paidRoutes[]` are generated from a curated 8-row constant instead of from the full
paid-route table, which is why the live catalog shows eight pricing rows while the API sells 18 routes. The
complete per-route price list is in `routes.md`, `/openapi.json` and every 402 challenge, and the parity test
covers those three plus the edge catalog — but it does not cover `pricing[]`, so the drift went untested. The
fix is to derive `pricing[]` from the full route table and extend the parity test to assert coverage of every
paid route. That touches the advertised price surface, so it ships through our own review; it will be named
here once it is live.

**Intermittent non-challenge responses (disclosed, not fixed):** during the sweep above the same hostname
answered something other than the challenge for a 75-second window — 137 of 145 probes to
`POST /v2/security/preflight` returned `404` with the edge's own fallback body
(`{"error":"not_found","path":"…","x402Version":2,"accepts":[…]}`) instead of `402`, and in a later window
`/stats` and `/openapi.json` returned the same fallback while `/pricing` answered normally. Immediate
re-probing returned `402`/`200` as expected (175 of 177, then 822 of 823). The fallback decides that the
upstream could not be reached or answered `5xx`; the cause is not proven from the outside, and it is named
here rather than presented as fixed. Anyone who prices the paid surface during such a window can conclude
"route does not exist" — send us the timestamp and we will correlate it instead of being listed as drift.
