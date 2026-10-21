# Agent Kiosk
- Type: API / AI agent (seller; not a facilitator)
- Description: 24-in-1 pay-per-call B2A intelligence, action calldata & compliance supermarket and MCP server on Base Mainnet (23 paid per-call endpoints from $0.001 to $0.10 USDC + 1 $5.00 30-day Prepaid API Pass, plus free discovery, telemetry, MCP teaser & partner-fee swap routes). Every paid and prepaid response includes an HMAC-SHA256 attestation envelope.
- Website (HTTPS): https://agent-kiosk.vercel.app
- Logo (HTTPS): https://agent-kiosk.vercel.app/favicon.ico
- Documentation: https://agent-kiosk.vercel.app/llms.txt (Catalogue & Buyer Guide), https://agent-kiosk.vercel.app/llms-full.txt (Full Schemas), https://agent-kiosk.vercel.app/openapi.json (OpenAPI 3.1), https://github.com/ralf9090/agent-kiosk#readme
- Public repository: https://github.com/ralf9090/agent-kiosk
- Networks and chain identifiers: Base Mainnet (eip155:8453) only.
- Paid resource URLs and HTTP methods: 24 x402-protected routes (23 paid per-call endpoints + 1 prepaid 30-day pass endpoint), plus free routes. All /v1/* x402 endpoints accept POST (primary JSON body) and GET (query parameters); live machine-readable list at https://agent-kiosk.vercel.app/.well-known/x402.json and https://agent-kiosk.vercel.app/openapi.json:

  | # | Category | Route | HTTP Method | Price (USDC) | Atomic Units (6 dec) | MCP Tool Name |
  |---|---|---|---|---|---|---|
  | 1 | Paid Per-Call | `https://agent-kiosk.vercel.app/v1/ping` | `POST` (or `GET`) | `$0.001` | `1000` | `x402_ping` |
  | 2 | Paid Per-Call | `https://agent-kiosk.vercel.app/v1/chat/completions` | `POST` (or `GET`) | `$0.002` | `2000` | `llm_chat_completions` |
  | 3 | Paid Per-Call | `https://agent-kiosk.vercel.app/v1/tx-simulate` | `POST` (or `GET`) | `$0.005` | `5000` | `evm_tx_simulator` |
  | 4 | Paid Per-Call | `https://agent-kiosk.vercel.app/v1/funding-rates` | `POST` (or `GET`) | `$0.008` | `8000` | `perp_funding_arbitrage` |
  | 5 | Paid Per-Call | `https://agent-kiosk.vercel.app/v1/macro-radar` | `POST` (or `GET`) | `$0.008` | `8000` | `tradfi_macro_radar` |
  | 6 | Paid Per-Call | `https://agent-kiosk.vercel.app/v1/web-extract` | `POST` (or `GET`) | `$0.01` | `10000` | `web_extract` |
  | 7 | Paid Per-Call | `https://agent-kiosk.vercel.app/v1/package-audit` | `POST` (or `GET`) | `$0.01` | `10000` | `package_audit` |
  | 8 | Paid Per-Call | `https://agent-kiosk.vercel.app/v1/github-intel` | `POST` (or `GET`) | `$0.01` | `10000` | `github_intel` |
  | 9 | Paid Per-Call | `https://agent-kiosk.vercel.app/v1/prediction-arb` | `POST` (or `GET`) | `$0.015` | `15000` | `kalshi_polymarket_arb` |
  | 10 | Paid Per-Call | `https://agent-kiosk.vercel.app/v1/social-search` | `POST` (or `GET`) | `$0.02` | `20000` | `social_search` |
  | 11 | Paid Per-Call | `https://agent-kiosk.vercel.app/v1/security-audit` | `POST` (or `GET`) | `$0.02` | `20000` | `security_audit` |
  | 12 | Paid Per-Call | `https://agent-kiosk.vercel.app/v1/token-alpha` | `POST` (or `GET`) | `$0.02` | `20000` | `token_alpha` |
  | 13 | Paid Per-Call | `https://agent-kiosk.vercel.app/v1/domain-intel` | `POST` (or `GET`) | `$0.02` | `20000` | `domain_intel` |
  | 14 | Paid Per-Call | `https://agent-kiosk.vercel.app/v1/academic-search` | `POST` (or `GET`) | `$0.02` | `20000` | `academic_search` |
  | 15 | Paid Per-Call | `https://agent-kiosk.vercel.app/v1/prediction-markets` | `POST` (or `GET`) | `$0.02` | `20000` | `prediction_markets` |
  | 16 | Paid Per-Call | `https://agent-kiosk.vercel.app/v1/defi-yields` | `POST` (or `GET`) | `$0.02` | `20000` | `defi_yields` |
  | 17 | Paid Per-Call | `https://agent-kiosk.vercel.app/v1/maps-leads` | `POST` (or `GET`) | `$0.03` | `30000` | `maps_leads` |
  | 18 | Paid Per-Call | `https://agent-kiosk.vercel.app/v1/wallet-profiler` | `POST` (or `GET`) | `$0.03` | `30000` | `wallet_profiler` |
  | 19 | Paid Per-Call | `https://agent-kiosk.vercel.app/v1/compliance-check` | `POST` (or `GET`) | `$0.05` | `50000` | `compliance_check` |
  | 20 | Paid Per-Call | `https://agent-kiosk.vercel.app/v1/defi-swap-quote` | `POST` (or `GET`) | `$0.05` | `50000` | `defi_swap_quote` |
  | 21 | Paid Per-Call | `https://agent-kiosk.vercel.app/v1/token-due-diligence` | `POST` (or `GET`) | `$0.10` | `100000` | `token_due_diligence` |
  | 22 | Paid Per-Call | `https://agent-kiosk.vercel.app/v1/b2b-company-dossier` | `POST` (or `GET`) | `$0.10` | `100000` | `b2b_company_dossier` |
  | 23 | Paid Per-Call | `https://agent-kiosk.vercel.app/v1/whale-alpha-radar` | `POST` (or `GET`) | `$0.10` | `100000` | `whale_alpha_radar` |
  | 24 | Prepaid Pass (30d) | `https://agent-kiosk.vercel.app/v1/buy-pass` | `POST` (or `GET`) | `$5.00` | `5000000` | `buy_prepaid_pass` |
  | — | Free Route (25bps swap fee) | `https://agent-kiosk.vercel.app/v1/free-swap` | `POST` / `GET` | `$0.00` | `0` | — |
  | — | Free Discovery | `https://agent-kiosk.vercel.app/v1/models` | `GET` | `$0.00` | `0` | — |
  | — | Free Telemetry | `https://agent-kiosk.vercel.app/v1/stats` (`/stats`) | `GET` | `$0.00` | `0` | — |
  | — | MCP JSON-RPC | `https://agent-kiosk.vercel.app/mcp` | `POST` / `GET` | `$0.00` (Teaser) / Paid (Full) | — | All 24 tools |

- x402 version and payment scheme: x402 v2 (x402 v1 also accepted), `exact` scheme (EIP-3009 `TransferWithAuthorization`).
- Token contract or mint, decimals: Base Mainnet USDC `0x833589fCD6eDb6E08f4c7C32D4f71b54bdA02913`, 6 decimals.
- Seller payment recipient addresses: `0xd8429209Aee6A398B9707DFf5F28AAA93452eE95` (Base Mainnet).
- Facilitator URL and supported endpoint (we are not the facilitator):

  | Role | Facilitator | Base URL | Supported | Verify | Settle | Supported Schemes |
  |---|---|---|---|---|---|---|
  | **Primary** | **PayAI Network** | `https://facilitator.payai.network` | `GET https://facilitator.payai.network/supported` | `POST https://facilitator.payai.network/verify` | `POST https://facilitator.payai.network/settle` | x402 v2 (`eip155:8453`, `exact`) & v1 (`base`, `exact`), no API key required |
  | **Fallback 1** | **Dexter** | `https://facilitator.dexter.cash` | `GET https://facilitator.dexter.cash/supported` | `POST https://facilitator.dexter.cash/verify` | `POST https://facilitator.dexter.cash/settle` | x402 v2 (`eip155:8453`, `exact`) & v1 (`base`, `exact`) |
  | **Fallback 2** | **Mogami** | `https://facilitator.mogami.tech` | `GET https://facilitator.mogami.tech/supported` | `POST https://facilitator.mogami.tech/verify` | `POST https://facilitator.mogami.tech/settle` | x402 v1 (`base`, `exact`) |

- Facilitator signer / relayer addresses (not Agent Kiosk addresses; separate from the `payTo` merchant address above):
  - **PayAI Network Base relayers** (listed in `GET https://facilitator.payai.network/supported` under `signers["eip155:*"]`): `0xc6699d2aadA6c36Dfea5C248DD70f9CB0235cB63` (submitted the `/v1/token-alpha` settlement below), `0xB2Bd29925CBbCEA7628279c91945Ca5B98bf371B` (submitted the `/v1/ping` settlement below), and pool signers `0x25659315106580ce2A787CeeC5efB2d347B539C9`, `0xB8F41cB13b1f213da1E94E1b742ec1323235C48F`, `0xe575fA51af90957d66FaB6d63355F1eD021b887b`.
  - **Dexter Base relayer:** `0x402Feee072D655B85e08f1751AF9ddbCd249521f`.
- Accepted payment/receipt headers & buyer recovery summary (documented in https://github.com/ralf9090/agent-kiosk#2-production-x402-buyer-guide--facilitator-integration and https://agent-kiosk.vercel.app/llms.txt):
  - **402 Challenge Header:** `PAYMENT-REQUIRED` (Base64-encoded x402 v2 JSON `PaymentRequired` payload, `maxTimeoutSeconds: 60`).
  - **Accepted Request Payment Headers:** `PAYMENT-SIGNATURE` (x402 v2 Base64/Base64URL/JSON), `X-PAYMENT` (x402 v1), or `X-PAYMENT-SIGNATURE` (or `payment_signature` / `x_payment` in MCP `tools/call` arguments). Prepaid pass holders pass `X-API-KEY: ak_live_...` or `Authorization: Bearer ak_live_...`.
  - **200 Settlement Receipt Headers:** `PAYMENT-RESPONSE` and `X-PAYMENT-RESPONSE` (Base64-encoded JSON receipt `{"success":true,"transaction":"0x...","network":"eip155:8453","payer":"0x..."}`, plus `tx_hash` in the HTTP 200 JSON body).
  - **Timeouts & Uncertain Settlement Recovery:** Server-side timeouts are `6.5s` for `/verify` and `10.0s` for `/settle` with automatic failover across configured facilitators. Because each EIP-3009 authorization binds a unique 32-byte `nonce`, buyers experiencing a network drop or HTTP timeout must first check `authorizationState(payer, nonce)` on Base USDC (`0x833589fCD6eDb6E08f4c7C32D4f71b54bdA02913`) or BaseScan before signing a new `nonce`. If unsettled on-chain, retry with the identical `PAYMENT-SIGNATURE` header before `validBefore`; if settled on-chain during a drop, report `txHash` at https://github.com/ralf9090/agent-kiosk/issues for replay/credit.
- Example successful settlement hashes and explorer links (operator test payments against live production https://agent-kiosk.vercel.app settled on Base Mainnet via PayAI Network facilitator; not third-party customer volume):
  1. **`POST https://agent-kiosk.vercel.app/v1/token-alpha` — `0.02 USDC` (`20000` atomic units), 2026-10-19:**
     - **BaseScan TX:** https://basescan.org/tx/0x5aa1b42ef7dae5323ba561b9374e9e5db0d42b0eae23d7e4fc5c2f0929df61be (Base Block `52809684`, Status: `Success`, Relayer: `0xc6699d2aadA6c36Dfea5C248DD70f9CB0235cB63`)
     - **Decoded `PAYMENT-RESPONSE` Receipt:** `{"success":true,"transaction":"0x5aa1b42ef7dae5323ba561b9374e9e5db0d42b0eae23d7e4fc5c2f0929df61be","network":"eip155:8453","payer":"0xd8429209aee6a398b9707dff5f28aaa93452ee95"}`
     - **Redacted HTTP 200 Resource Response:** `{"ok":true,"payment_mode":"x402","tx_hash":"0x5aa1b42ef7dae5323ba561b9374e9e5db0d42b0eae23d7e4fc5c2f0929df61be","attestation":{"attested":true,"issuer":"io.github.ralf9090/agent-kiosk","signer_wallet":"0xd8429209Aee6A398B9707DFf5F28AAA93452eE95","algorithm":"HMAC-SHA256","route":"/v1/token-alpha","payload_sha256":"c1bcebf107e25a742a7afc58ca39692bc33f4e6da49a2ca1afc8b892fae63a1f","timestamp_utc":"2026-10-19T11:18:33.296Z","signature":"<REDACTED>"},"data":{"query":"AERO","found":true,"token":{"name":"Aerodrome","symbol":"AERO","address":"0x940181a94A35A4569E4529A3CDfB74e38FD98631","primary_chain":"base","price_usd":0.7866},"alpha_metrics":{"signal":"SELL_PRESSURE","total_top5_liquidity_usd":47963273,"volume_24h_usd":12606349}}}`
  2. **`POST https://agent-kiosk.vercel.app/v1/ping` — `0.001 USDC` (`1000` atomic units), 2026-10-19:**
     - **BaseScan TX:** https://basescan.org/tx/0xd4869a2190887c15b9fb53c109045fe60bb6bef6a3cf8b66e6f7e0a9904fda7e (Base Block `52809683`, Status: `Success`, Relayer: `0xB2Bd29925CBbCEA7628279c91945Ca5B98bf371B`)
     - **Decoded `PAYMENT-RESPONSE` Receipt:** `{"success":true,"transaction":"0xd4869a2190887c15b9fb53c109045fe60bb6bef6a3cf8b66e6f7e0a9904fda7e","network":"eip155:8453","payer":"0xd8429209aee6a398b9707dff5f28aaa93452ee95"}`
     - **Redacted HTTP 200 Resource Response:** `{"ok":true,"payment_mode":"x402","tx_hash":"0xd4869a2190887c15b9fb53c109045fe60bb6bef6a3cf8b66e6f7e0a9904fda7e","attestation":{"attested":true,"issuer":"io.github.ralf9090/agent-kiosk","signer_wallet":"0xd8429209Aee6A398B9707DFf5F28AAA93452eE95","algorithm":"HMAC-SHA256","route":"/v1/ping","payload_sha256":"6fc2d484b7899b71b18d80b87c18230e8904e7f296ca3c471763cc618a932041","timestamp_utc":"2026-10-19T11:18:31.280Z","signature":"<REDACTED>"},"data":{"status":"pong","verified":true,"payment_mode":"x402","service":"Agent Kiosk","version":"2.6.0","network":"eip155:8453","asset":"USDC","echo":"x402-registry-verification","payer":"0xd8429209Aee6A398B9707DFf5F28AAA93452eE95","tx_hash":"0xd4869a2190887c15b9fb53c109045fe60bb6bef6a3cf8b66e6f7e0a9904fda7e"}}`
- Ownership evidence (domain-hosted proof or public project reference):
  - Domain manifest: https://agent-kiosk.vercel.app/.well-known/x402.json
  - Public repository: https://github.com/ralf9090/agent-kiosk (authored by the same GitHub account `ralf9090` submitting this PR, naming `0xd8429209Aee6A398B9707DFf5F28AAA93452eE95` as `payTo`).
- Public support channel: https://github.com/ralf9090/agent-kiosk/issues
