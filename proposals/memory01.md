# Memory01

## Basic details
- Project name: Memory01
- What does it do? (2–3 sentences): Agentic memory service for AI agents. Free to store memories (key-value with metadata). Free for the first 30 semantic searches/day per agent, then paid to search with $0.01 USDC per search via x402 on Base. Write-token + optional Ed25519 key-bound authentication ensures memory isolation — no one can read your memories without your token. Subscription plans available: Starter (non-expiring credits), Pro and Enterprise (monthly subscription credits).
- Type: API
- Official website: https://memory.node01.org/
- Logo URL: https://memory.node01.org/favicon.ico
- Documentation or getting-started link: https://memory.node01.org/llms.txt (OpenAPI: https://memory.node01.org/openapi.json; agents.md: https://memory.node01.org/agents.md; x402: https://memory.node01.org/.well-known/x402)
- Public support channel: enrico@node01.org

## Networks and activity
- Networks: Base
- Public explorer or analytics link, if available: https://www.x402scan.com/server/eb0ca4e3-4f4b-4912-ab75-a8f26fa61416 (origin registered); operator self-pay settlement linked in evidence below
- App contract/program or receiving addresses, with their networks, if available: Base (eip155:8453) payee 0xe9a827d9453e9b18040c25bb492a568ddd827549
- Proof that you represent the project: domain ownership (memory.node01.org resolves to our server); service-hosted submitting account: https://github.com/node01-dev ; operator contact: enrico@node01.org
- Official X account: none

## Payments — only if your product accepts payments
- Paid endpoint and HTTP method: POST /api/memory/search ($0.01 USDC per search after 30 free/day), POST /api/memory/subscribe (paid plan)
- Full paid URLs: https://memory.node01.org/api/memory/search , https://memory.node01.org/api/memory/subscribe
- Payment version/scheme: x402 v2, `exact` scheme
- Network: eip155:8453 (Base mainnet)
- Native USDC contract + decimals: 0x833589fCD6eDb6E08f4c7C32D4f71b54bdA02913 , 6 decimals
- Facilitator URL + auth: https://facilitator.payai.network (keyless; no facilitator authentication)
- Settlement address(es): 0xe9a827d9453e9b18040c25bb492a568ddd827549 (Base)
- Payment headers: canonical `PAYMENT-SIGNATURE` (x402 v2); legacy alias `X-Payment` (and `payment-signature`) accepted. 402 returns `PAYMENT-REQUIRED` (base64 + JSON body `accepts[]`). 200 returns `PAYMENT-RESPONSE` (base64 success/transaction/network/payer) + `settlement_tx`.
- Request/result/payment correlation (operator self-pay, redacted): see `proposals/memory01-evidence.json`
  - named route POST /api/memory/search, $0.01, tx https://basescan.org/tx/0x53152ba5fdb55ec8c77097dc8a65bb676b8ab3e16ddf1f86bf0b30e3db386bee
  - decoded PAYMENT-RESPONSE success=true, network eip155:8453, payer=payTo=0xe9a827d9453e9b18040c25bb492a568ddd827549, transaction matches on-chain USDC transfer (amount 10000 atomic = 0.01 USDC), request/result retained (write_token + reusable signed payment redacted). **Operator test**, no independent customer demand required.

### Plan / credit / rate-limit figures (consistent across llms.txt, homepage, OpenAPI, this proposal)
- Free: 30 searches/day, no payment. Store always free.
- Starter: $2 USDC one-time → 500 search credits, **non-expiring** (not monthly); 200/day rate-limit cap.
- Pro: $9/month subscription → **monthly subscription credits** reset each 30-day period (not non-expiring); 500/day rate-limit cap (slowdown after 100).
- Enterprise: $20/month subscription → **monthly subscription credits** reset each 30-day period (not non-expiring); 2000/day rate-limit cap (slowdown after 500).
- Monthly subscription credits are distinct from Starter's non-expiring credits; monthly subscription credits do not roll over.

### Recovery after settlement (no blind second payment)
- No automatic refund; on-chain settlement is final. But no blind second payment is required to verify a lost result: retain the request, the actual response, the decoded PAYMENT-RESPONSE (success/transaction/network/payer) and the on-chain tx; that correlation proves payment independently.
- Replay cache / cursor: `next_cursor` is pagination only, TTL 10s (CURSOR_TTL), bound to `write_token` (not IP); expired cursor returns HTTP 410 `cursor_expired`; it does not restore a lost paid first-page result. The first page is paid; subsequent pages use the cursor.
- Subscription token lost: `POST /api/memory/recover` {agent_id, recovery_code} → new write_token bound to current IP keeping agent_id; credits + subscription keyed by agent_id. `POST /api/memory/recovery/regenerate` {write_token} → fresh recovery code (old invalidated). No second payment to recover an already-paid subscription.
- Payer IP changes: use key-bound auth — `POST /api/memory/register-key` {agent_id, write_token, public_key} (Ed25519), sign requests with X-Agent-Id/X-Agent-Timestamp/X-Agent-Nonce/X-Agent-Signature; token then works from any IP. Without key-bound auth, token is bound to (IP, agent_id); on IP change use `/api/memory/recover`. Settlement payment itself is not invalidated by IP change; subscription recovery needs no new payment.
- Authentication + retention: write_token private; recovery_code shown once; credentials at ~/.memory01_token / ~/.memory01_recovery / ~/.memory01_key chmod 600; memory stores only a `credentials-location` pointer, never secrets; memories + subscription retained (no automatic deletion; no IP-based loss if key-bound or recovery used). No reusable signed payment authorizations or private keys are exposed.

## Refund / dispute policy
No refunds for completed searches. Payment is final on-chain; verify via PAYMENT-RESPONSE + tx. Subscription credits per plan rules above.

## Ownership reference
- Submitting account (service-hosted): https://github.com/node01-dev
- Contact email: enrico@node01.org
- Domain: memory.node01.org (DNS resolves to our server)
- Official X account: none
