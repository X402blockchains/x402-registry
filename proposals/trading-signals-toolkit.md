# Trading Signals Toolkit

## Basic details
- Project name: Trading Signals Toolkit
- What does it do? (2–3 sentences): Pay-per-call data API and remote MCP server for AI agents and traders. Its crypto routes return a token risk verdict for Base tokens (holder concentration, liquidity, live sell-route test), 24h whale flow (large DEX buys vs sells, net flow, top wallets), OFAC address screening and wallet pay-readiness. Agents pay per call in USDC over x402 with no signup or API key.
- Type: API (plus a remote MCP server)
- Official website: https://signals.incomefather.com
- Logo URL: https://signals.incomefather.com/favicon-32.png (social card: https://signals.incomefather.com/og-image.png)
- Documentation or getting-started link: https://signals.incomefather.com/llms.txt , https://signals.incomefather.com/openapi.json , https://signals.incomefather.com/guides/crypto-whale-flow-api
- Public support channel: https://signals.incomefather.com/support (email listed there) and https://github.com/gdietsch/trading-signals-mcp/issues
- Official X profile: **@TradingSignalsA** — https://x.com/TradingSignalsA (also listed under "Official channels" on https://signals.incomefather.com/payments)
- Buyer recovery (uncertain settlement, paid but no result): https://signals.incomefather.com/payments

## Networks and activity
- Networks requested for this initial listing: **Base only (eip155:8453)**.
- **Out of scope: Solana.** The live server also advertises a Solana payment option through PayAI. We have no retained successful Solana x402 settlement to evidence, so Solana payments are excluded from this initial listing. We are not asking for Solana to be listed and will open a separate request if that changes.
- Public explorer or analytics link, if available: https://www.x402scan.com/ (listed), https://basescan.org/address/0x6d7be981c103eD360874a7703ad3CD6a98929aFB#tokentxns
- App contract/program or receiving addresses, with their networks, if available:
  - Base: 0x6d7be981c103eD360874a7703ad3CD6a98929aFB
- Proof that you represent the project (official website, repository or public announcement): this PR is opened by the owner of https://github.com/gdietsch/trading-signals-mcp , the MCP client package published to npm as trading-signals-mcp and to the MCP Registry as io.github.gdietsch/trading-signals-mcp, which points at https://signals.incomefather.com/mcp

## Payments — only if your product accepts payments
- Paid endpoint and HTTP method (Base payments; these are the three routes in the evidence below):
  - GET https://signals.incomefather.com/base/token-verdict?address=<address> (0.01 USDC)
  - GET https://signals.incomefather.com/crypto/whale-flow?token=<token>&hours=24 (0.02 USDC)
  - GET https://signals.incomefather.com/bundle/token-pre-trade?token=<token> (0.015 USDC)
  - Full route list: https://signals.incomefather.com/openapi.json
- Facilitator used: Coinbase CDP (primary on Base, and the only facilitator in the evidence below). PayAI is configured as a fallback only.
- Payment scheme/version: x402 v2, exact
- Token contract/mint and decimals: USDC on Base 0x833589fCD6eDb6E08f4c7C32D4f71b54bdA02913 (6 decimals)
- Successful payment transaction link for each supported network: Base, see "Settlement evidence (Base)" below.

### Settlement evidence (Base) — OPERATOR TESTS

All three are **operator tests**: paid by our own listing wallet `0xfDEbA0DDe0A97DFc0b2820f6a624c5A4c6e167C8` from `ops/listing-buys.mjs` (x402 v2 `exact`, `@x402/fetch` client) against the production server. They are not third-party purchases. No new payment was made for this follow-up. Everything below is retained data; nothing was re-run or reconstructed.

| # | Route / method | Amount | Recipient | Facilitator | Tx (Base) | Block / time (UTC) |
|---|---|---|---|---|---|---|
| 1 | `GET /base/token-verdict?address=0x940181a94A35A4569E4529A3CDfB74e38FD98631` | 0.01 USDC (10000) | 0x6d7be981c103eD360874a7703ad3CD6a98929aFB | Coinbase CDP | [0x7395d1c4…b41b47d6e](https://basescan.org/tx/0x7395d1c4f346d5bb629a11c5afcc53b9aa472717f6c194d751e44b7d41b47d6e) | 57122369 / 2026-11-14 00:07:29 |
| 2 | `GET /crypto/whale-flow?token=DezXAZ8z7PnrnRJjz3wXBoRgixCa6xjnB7YaB1pPB263` | 0.02 USDC (20000) | 0x6d7be981c103eD360874a7703ad3CD6a98929aFB | Coinbase CDP | [0x7324d82a…39ba765c](https://basescan.org/tx/0x7324d82aa2b4482202daae23b89eb6f5c9d6b2864f918cc7e654107039ba765c) | 57124767 / 2026-11-14 00:15:29 |
| 3 | `GET /bundle/token-pre-trade?token=DezXAZ8z7PnrnRJjz3wXBoRgixCa6xjnB7YaB1pPB263&wallet=0x6d7be981c103eD360874a7703ad3CD6a98929aFB&amount=0.01` | 0.015 USDC (15000) | 0x6d7be981c103eD360874a7703ad3CD6a98929aFB | Coinbase CDP | [0xbef7d7a5…6e61a8b4](https://basescan.org/tx/0xbef7d7a5a11025c04d6c2aafe7d3cd83ab6fccba319009d13d2195bc6e61a8b4) | 57128228 / 2026-11-14 00:27:01 |

Note on #2 and #3: the `token` query value is the data being looked up. The payment for every row is USDC on Base; none of these is a Solana payment.

#### A. Public, independently checkable (on chain)

Decoded from the Base receipts (re-checked 2026-11-26 against `https://mainnet.base.org`). Each tx calls USDC `transferWithAuthorization` (selector `0xe3ee160e`), status 1, and emits exactly one USDC `Transfer` and one `AuthorizationUsed`:

| # | Tx sender (facilitator relayer) | Transfer from → to | Value | `AuthorizationUsed` authorizer / nonce |
|---|---|---|---|---|
| 1 | 0x67b9ce703d9ce658d7c4ac3c289cea112fe662af | 0xfDEb…67C8 → 0x6d7b…9aFB | 10000 | 0xfDEb…67C8 / `0xc61e1c48b56e429e3174027e55d000f00ea5466b3771de996b90c63f5cd6f027` |
| 2 | 0x625d8a65134079f8faaac39a7947c73d93c6ac39 | 0xfDEb…67C8 → 0x6d7b…9aFB | 20000 | 0xfDEb…67C8 / `0x92bacd5455135c8c83ea99ff1e68147fc715d8037434bab3674504e7c51a6fa5` |
| 3 | 0x772003a2e9c2ccc8af956870a37a66f64f8cec38 | 0xfDEb…67C8 → 0x6d7b…9aFB | 15000 | 0xfDEb…67C8 / `0x432715d52ab0e2984a3cf46f7e20c50d47a2b85af5131394dab4026cf40a8d90` |

To check one yourself (any Base RPC, no key needed):
```
curl -s https://mainnet.base.org -H 'content-type: application/json' \
  -d '{"jsonrpc":"2.0","id":1,"method":"eth_getTransactionReceipt","params":["0x7395d1c4f346d5bb629a11c5afcc53b9aa472717f6c194d751e44b7d41b47d6e"]}'
```
In `logs`, the USDC entry with topic `0xddf252ad…` is the Transfer (topics 1/2 = from/to, data = value); the entry with topic `0x98de5035…` is `AuthorizationUsed` (topic 1 = authorizer, topic 2 = nonce). These nonces are already consumed on chain, so they cannot be settled again. The relayer addresses are not in PayAI's published signer list (https://facilitator.payai.network/supported).

#### B. Retained operator records (not independently verifiable)

B1. Client log, `ops/listing-buys.log`, verbatim lines (the `PAYMENT-SIGNATURE` request header was never logged and is not shown):
```
{"at":"2026-11-14T00:07:29.567Z","route":"GET /base/token-verdict","status":200,"ms":3468,"priceUsd":0.01,"tx":"0x7395d1c4f346d5bb629a11c5afcc53b9aa472717f6c194d751e44b7d41b47d6e","basescan":"https://basescan.org/tx/0x7395d1c4f346d5bb629a11c5afcc53b9aa472717f6c194d751e44b7d41b47d6e","receipt":{"success":true,"payer":"0xfDEbA0DDe0A97DFc0b2820f6a624c5A4c6e167C8","transaction":"0x7395d1c4f346d5bb629a11c5afcc53b9aa472717f6c194d751e44b7d41b47d6e","network":"eip155:8453"},"bodyBytes":7658}
{"at":"2026-11-14T00:15:29.177Z","route":"GET /crypto/whale-flow","status":200,"ms":3742,"priceUsd":0.02,"tx":"0x7324d82aa2b4482202daae23b89eb6f5c9d6b2864f918cc7e654107039ba765c","basescan":"https://basescan.org/tx/0x7324d82aa2b4482202daae23b89eb6f5c9d6b2864f918cc7e654107039ba765c","receipt":{"success":true,"payer":"0xfDEbA0DDe0A97DFc0b2820f6a624c5A4c6e167C8","transaction":"0x7324d82aa2b4482202daae23b89eb6f5c9d6b2864f918cc7e654107039ba765c","network":"eip155:8453"},"bodyBytes":5069}
{"at":"2026-11-14T00:27:01.486Z","route":"GET /bundle/token-pre-trade","status":200,"ms":2058,"priceUsd":0.015,"tx":"0xbef7d7a5a11025c04d6c2aafe7d3cd83ab6fccba319009d13d2195bc6e61a8b4","basescan":"https://basescan.org/tx/0xbef7d7a5a11025c04d6c2aafe7d3cd83ab6fccba319009d13d2195bc6e61a8b4","receipt":{"success":true,"payer":"0xfDEbA0DDe0A97DFc0b2820f6a624c5A4c6e167C8","transaction":"0xbef7d7a5a11025c04d6c2aafe7d3cd83ab6fccba319009d13d2195bc6e61a8b4","network":"eip155:8453"},"bodyBytes":2089}
```
`receipt` is the decoded `PAYMENT-RESPONSE` header that came back on the same HTTP 200 response as the body. `bodyBytes` is the size of that body. The body itself was not saved.

B2. Server log (production, Railway deployment `cc197401`). It is written when the 2xx response finishes. The fields come from the `PAYMENT-RESPONSE` header set on that same response object. No raw IP, query string or body is stored. Verbatim line for #1:
```
2026-11-14T00:07:29.446Z usage {"ts":"2026-11-14T00:07:29.442Z","kind":"paid","name":"GET /base/token-verdict","status":200,"ua":"node","payer":"0xfDEbA0DDe0A97DFc0b2820f6a624c5A4c6e167C8","network":"eip155:8453","tx":"0x7395d1c4f346d5bb629a11c5afcc53b9aa472717f6c194d751e44b7d41b47d6e","amount":"10000","plan":"x402"}
```
For #2 and #3, the same fields were recorded at 2026-11-14T00:15:29.045Z (`GET /crypto/whale-flow`, 20000, tx 0x7324d82a…) and 2026-11-14T00:27:01.316Z (`GET /bundle/token-pre-trade`, 15000, tx 0xbef7d7a5…). Their full log lines were not copied verbatim when they were written, so we show only these fields. The matching rows are still in the operator's 90-day `usage_events` table. On 2026-11-26 an aggregate check showed one paid row each for these three routes from payer 0xfDEb…67C8. Under the 90-day rule they will be deleted around 2027-02-12.

B3. Facilitator: each of those deployments logged `facilitator=cdp https://api.cdp.coinbase.com/platform/v2/x402` at boot. Base settlement goes to CDP first; PayAI is used only if CDP fails to start.

#### C. Exactly how request, result and transaction are bound, and what is NOT established

- **Transaction ↔ payment (immutable, public):** tx hash → one `Transfer` of the exact route price from the payer to our payTo, plus one consumed EIP-3009 nonce (section A).
- **Request ↔ transaction (operator-held, not immutable):** the tx hash appears in (a) the `PAYMENT-RESPONSE` header the client received on the HTTP 200 for that route (B1) and (b) the server's paid-call record for that route (B2). The amount in each record equals that route's advertised price, and the times match the block time to the second. EIP-3009 transfers carry no memo, so **the chain itself does not record the route or the request**; that link exists only in our logs. The client did not log the signed nonce, so the nonce cannot be matched to a specific client request beyond the tx hash.
- **Delivered result:** HTTP status 200 and body size only. **We did not retain the response bodies, and there is no hash or signature of their content.** We therefore cannot show or prove what content was delivered for these three calls, and we have not rebuilt or re-run them to fill the gap. Re-calling the routes now would return current data, not the historical result.
- Not shown, by design: the signed `PAYMENT-SIGNATURE` payloads (never logged), private keys and API credentials.

### Buyer recovery (settled call, response lost)

Final instructions, published at https://signals.incomefather.com/payments (linked from https://signals.incomefather.com/support and /terms). This describes what the server does today (`@x402/express` 2.30), not an extra guarantee:

1. **How charging works:** the payment is verified before the route runs, and the response is held in memory. It is settled **only** after a 2xx result. A 4xx/5xx result is not settled. If settlement fails, the result is discarded and HTTP 402 is returned. Each signed authorization has a one-time nonce and an expiry, so one signature cannot be charged twice.
2. **Before paying again, check whether you were charged:** look on Basescan for a USDC transfer from your payer to `0x6d7be981c103eD360874a7703ad3CD6a98929aFB` around the time of the call, or read `authorizationState(payer, nonce)` on the USDC contract. If no transfer exists, you were not charged. **If a transfer exists, do not pay again; contact support first.**
3. **Report it:** email the address on https://signals.incomefather.com/support, or open an issue at https://github.com/gdietsch/trading-signals-mcp/issues. Include the tx hash, route, payer address and approximate time. Never send private keys, API keys or a signed payment header.
4. **What we check:** our paid-call record for that tx (route, status, payer, network, amount, tx hash), and whether a 2xx result was produced. We reply with what we find. There is no response-time guarantee.
5. **Limits, stated plainly:**
   - Results are not cached and request/response bodies are not stored, so **there is no replay or re-download of a lost result**. A new request is a new call.
   - Paid-call records are kept for **90 days** and then deleted. After that we can only check the public chain record.
   - Any remedy, such as returning the amount to the paying address, is decided case by case by the operator. **There is no automatic refund.**
- Facilitator applicants: Not applicable (not a facilitator)

## Website application
- Website application reference, if you have one: none
- Related issue or previous pull request, if any: none
