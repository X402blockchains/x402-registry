# Trading Signals Toolkit

## Basic details
- Project name: Trading Signals Toolkit
- What does it do? (2–3 sentences): Pay-per-call data API and remote MCP server for AI agents and traders. Its crypto routes return a safe/caution/avoid token verdict for Base and Solana tokens (mint/freeze authority, Token-2022 extensions, top-holder concentration, sniper/bundle wallets, liquidity and LP lock, live sell-route test), 24h whale flow (large DEX buys vs sells, net flow, top wallets), OFAC address screening and wallet pay-readiness. Agents pay per call in USDC over x402 with no signup or API key.
- Type: API (plus a remote MCP server)
- Official website: https://signals.incomefather.com
- Logo URL: https://signals.incomefather.com/favicon-32.png (social card: https://signals.incomefather.com/og-image.png)
- Documentation or getting-started link: https://signals.incomefather.com/llms.txt , https://signals.incomefather.com/openapi.json , https://signals.incomefather.com/guides/solana-token-safety-check-api , https://signals.incomefather.com/guides/crypto-whale-flow-api
- Public support channel: https://github.com/gdietsch/trading-signals-mcp/issues
- Official X profile: https://x.com/TradingSignalsA
- Buyer recovery (uncertain settlement, paid but no result): https://signals.incomefather.com/payments

## Networks and activity
- Networks requested for this initial listing: **Base only (eip155:8453)**. Scope narrowed on 2026-11-15: the server also advertises Solana mainnet through PayAI, but we have no retained successful Solana x402 settlement to evidence, so Solana is not part of this application.
- Public explorer or analytics link, if available: https://www.x402scan.com/ (listed), https://basescan.org/address/0x6d7be981c103eD360874a7703ad3CD6a98929aFB#tokentxns
- App contract/program or receiving addresses, with their networks, if available:
  - Base: 0x6d7be981c103eD360874a7703ad3CD6a98929aFB
- Proof that you represent the project (official website, repository or public announcement): this PR is opened by the owner of https://github.com/gdietsch/trading-signals-mcp , the MCP client package published to npm as trading-signals-mcp and to the MCP Registry as io.github.gdietsch/trading-signals-mcp, which points at https://signals.incomefather.com/mcp

## Payments — only if your product accepts payments
- Paid endpoint and HTTP method:
  - GET https://signals.incomefather.com/solana/token-verdict?mint=<mint> (0.01 USDC)
  - GET https://signals.incomefather.com/base/token-verdict?address=<address> (0.01 USDC)
  - GET https://signals.incomefather.com/crypto/whale-flow?token=<address or mint>&hours=24 (0.02 USDC)
  - GET https://signals.incomefather.com/bundle/token-pre-trade?token=<address or mint> (0.015 USDC)
  - Full route list: https://signals.incomefather.com/openapi.json
- Facilitator used: Coinbase CDP (primary on Base, the only facilitator in the evidence below). PayAI is configured as a fallback only.
- Payment scheme/version: x402 v2, exact
- Token contract/mint and decimals: USDC on Base 0x833589fCD6eDb6E08f4c7C32D4f71b54bdA02913 (6 decimals)
- Successful payment transaction link for each supported network: Base, see "Settlement evidence (Base)" below.

### Settlement evidence (Base) — OPERATOR TESTS

All three are **operator tests**: paid by our own listing wallet `0xfDEbA0DDe0A97DFc0b2820f6a624c5A4c6e167C8` from `ops/listing-buys.mjs` (x402 v2 `exact`, `@x402/fetch` client) against the production server. They are not third-party purchases. No new payment was made for this follow-up; all data below is retained.

| # | Route / method | Amount | Recipient | Facilitator | Tx (Base) | Block / time (UTC) |
|---|---|---|---|---|---|---|
| 1 | `GET /base/token-verdict?address=0x940181a94A35A4569E4529A3CDfB74e38FD98631` | 0.01 USDC (10000) | 0x6d7be981c103eD360874a7703ad3CD6a98929aFB | Coinbase CDP | [0x7395d1c4…b41b47d6e](https://basescan.org/tx/0x7395d1c4f346d5bb629a11c5afcc53b9aa472717f6c194d751e44b7d41b47d6e) | 57122369 / 2026-11-14 00:07:29 |
| 2 | `GET /crypto/whale-flow?token=DezXAZ8z7PnrnRJjz3wXBoRgixCa6xjnB7YaB1pPB263` | 0.02 USDC (20000) | 0x6d7be981c103eD360874a7703ad3CD6a98929aFB | Coinbase CDP | [0x7324d82a…39ba765c](https://basescan.org/tx/0x7324d82aa2b4482202daae23b89eb6f5c9d6b2864f918cc7e654107039ba765c) | 57124767 / 2026-11-14 00:15:29 |
| 3 | `GET /bundle/token-pre-trade?token=DezXAZ8z7PnrnRJjz3wXBoRgixCa6xjnB7YaB1pPB263&wallet=0x6d7be981c103eD360874a7703ad3CD6a98929aFB&amount=0.01` | 0.015 USDC (15000) | 0x6d7be981c103eD360874a7703ad3CD6a98929aFB | Coinbase CDP | [0xbef7d7a5…6e61a8b4](https://basescan.org/tx/0xbef7d7a5a11025c04d6c2aafe7d3cd83ab6fccba319009d13d2195bc6e61a8b4) | 57128228 / 2026-11-14 00:27:01 |

Each on-chain tx is a single USDC (`0x833589fC…02913`) `transferWithAuthorization` Transfer from the payer to our payTo for exactly the amount above (receipt status 1).

**Request / result / payment correlation for #1** (same pattern for #2 and #3):

1. Client side, retained redacted successful result (operator log line; the `PAYMENT-SIGNATURE` request header is not logged and is withheld):
   ```json
   {"at":"2026-11-14T00:07:29.567Z","route":"GET /base/token-verdict","status":200,"ms":3468,"priceUsd":0.01,
    "receipt":{"success":true,"payer":"0xfDEbA0DDe0A97DFc0b2820f6a624c5A4c6e167C8",
               "transaction":"0x7395d1c4f346d5bb629a11c5afcc53b9aa472717f6c194d751e44b7d41b47d6e","network":"eip155:8453"},
    "bodyBytes":7658}
   ```
   `receipt` is the decoded `PAYMENT-RESPONSE` header returned with the HTTP 200. The 7,658-byte JSON body (the token verdict) was delivered to the client; only its size was retained, not its content.
2. Server side, production log line written when the 2xx response finished (Railway deployment `cc197401`, no raw IP or request body stored):
   ```
   2026-11-14T00:07:29.446Z usage {"ts":"2026-11-14T00:07:29.442Z","kind":"paid","name":"GET /base/token-verdict","status":200,"ua":"node","payer":"0xfDEbA0DDe0A97DFc0b2820f6a624c5A4c6e167C8","network":"eip155:8453","tx":"0x7395d1c4f346d5bb629a11c5afcc53b9aa472717f6c194d751e44b7d41b47d6e","amount":"10000","plan":"x402"}
   ```
   #2: same fields, ts 2026-11-14T00:15:29.045Z, `GET /crypto/whale-flow`, amount 20000, tx 0x7324d82a…, client bodyBytes 5069.
   #3: same fields, ts 2026-11-14T00:27:01.316Z, `GET /bundle/token-pre-trade`, amount 15000, tx 0xbef7d7a5…, client bodyBytes 2089.
3. Facilitator: each of those deployments logged `facilitator=cdp https://api.cdp.coinbase.com/platform/v2/x402` at boot, and Base settlement is routed to CDP first (PayAI only on CDP init failure). The settling senders (`0x67b9ce70…`, `0x625d8a65…`, `0x772003a2…`) are not in PayAI's published signer list (`https://facilitator.payai.network/supported`).
4. On chain: block time of each tx equals the server log second above.

### Buyer recovery

Documented at https://signals.incomefather.com/payments (also linked from /support and /terms). Summary of actual server behavior (`@x402/express` 2.30): verify before the handler, response held in memory, settle **only** after a 2xx result; a 4xx/5xx result is not settled; a failed settlement discards the result and returns 402. Signed authorizations are one-time nonces, so one signature cannot be charged twice. Results are not cached. For uncertain settlement, the buyer checks for a transfer to the payTo (or `authorizationState` on USDC) before re-signing. For a paid call with a lost result, the buyer opens a GitHub issue or emails with the tx hash; we check our 90-day paid-call log for that tx and reply. Remedies such as returning the amount are case by case; there is no automatic refund.
- Facilitator applicants: Not applicable (not a facilitator)

## Website application
- Website application reference, if you have one: none
- Related issue or previous pull request, if any: none
