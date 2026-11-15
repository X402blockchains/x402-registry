# AIPayGen

## Basic details
- Project name: AIPayGen
- What does it do? (2–3 sentences): Pay-per-call tools for AI agents (web and company intelligence, AI text and media, crypto, markets and reference data), served over HTTP and a remote MCP server. Agents also search a free marketplace of 19,000+ APIs, MCP servers, skills and agents. Each paid tool is paid per call with x402 (no account), or with prepaid credits.
- Type: API (plus a remote MCP server)
- Official website: https://aipaygen.com
- Logo URL: https://aipaygen.com/logo.svg
- Documentation or getting-started link: buyer guide https://aipaygen.com/buyers (routes, prices, facilitator, receipts, recovery); also https://aipaygen.com/llms.txt, OpenAPI https://aipaygen.com/openapi.json, MCP https://mcp.aipaygen.com/mcp, x402 discovery https://aipaygen.com/.well-known/x402
- Official X profile: https://x.com/aipaygen
- Public support channel: GitHub issues at https://github.com/Damien829/aipaygen/issues

## Networks and activity
- Networks: Base
- Public explorer or analytics link, if available: https://basescan.org/address/0xeba22e8cd05cb72a2f913099d6cca666dd6d35b0 (production receiving address). x402scan listing: https://www.x402scan.com (origin aipaygen.com, 146 resources registered 2026-11-14).
- App contract/program or receiving addresses, with their networks, if available: Base (eip155:8453) payee 0xeba22e8cd05cb72a2f913099d6cca666dd6d35b0 (current, production)
- Proof that you represent the project: see "Ownership reference" below.

## Payments — only if your product accepts payments
- Paid endpoint and HTTP method: GET or POST https://aipaygen.com/v1/{tool} for 88 paid tools. Reviewed example: POST https://aipaygen.com/v1/dns_lookup with {"domain": "example.com"}, price $0.001 (1000 atomic USDC). Each tool's fixed USD price is in its 402 quote, https://aipaygen.com/v1/tools and `x-payment-info` in the OpenAPI document. Free: https://aipaygen.com/v1/search_marketplace, docs, llms.txt.
- Free tier: each caller gets 3 free calls a day on tools priced $0.005 or less, which is why the earlier unpaid DNS check returned a free result. Send `X-AIPayGen-Free: off` to always get the 402 and pay.
- Facilitator used: Coinbase CDP (https://api.cdp.coinbase.com/platform/v2/x402). The live discovery document now reports the same value (`facilitator` in https://aipaygen.com/.well-known/x402). It previously showed PayAI because it printed a fallback setting instead of the facilitator actually in use; fixed 2026-11-15. Both test settlements below were submitted by CDP relayers.
- Payment scheme/version: x402 v2, exact (USDC transferWithAuthorization)
- Token contract/mint and decimals: USDC on Base, 0x833589fCD6eDb6E08f4c7C32D4f71b54bdA02913, 6 decimals
- Successful payment transaction link for each supported network: see "Payment example" below.
- Facilitator applicants: Not applicable to this application. AIPayGen also runs a facilitator (https://aipaygen.com/facilitator, setup guide https://aipaygen.com/merchants); a separate facilitator application will follow once it has settlements from its own signer.

## Website application
- Website application reference, if you have one: none
- Related issue or previous pull request, if any: none

## Original payment example (retained), OPERATOR TEST, not customer activity (Base mainnet)
- Request: an AIPayGen paid tool call, paid with x402
- Amount: 0.001 USDC (1000 atomic, 6 decimals) on Base mainnet (eip155:8453), 2026-11-14 12:52:56 UTC
- Payer: 0x55c27e9b8e70a37af15f57b284be4dc9aa26e617, the operator's own test wallet
- Transaction: https://basescan.org/tx/0x74d50969bc1748c2a6ca2ebd05c31fbdb9b686abf1cf6bd963a604996b7d9328 (block 57352002, status success; USDC Transfer 0x55c2…e617 → 0xeba2…35b0, 0.001 USDC; submitted by the CDP facilitator's relayer 0x93f6601151ccb08f333ab4b1cccfb1e188c0be44)
- This shows the production recipient and payment path work end to end; it is not presented as customer activity.

## Ownership reference
- This pull request is opened by GitHub account Damien829, which owns the source repository https://github.com/Damien829/aipaygen.
- The Official MCP Registry entry io.github.Damien829/aipaygen (GitHub-verified namespace, version 2.3.0) lists the remote https://mcp.aipaygen.com/mcp and website https://aipaygen.com.

## Paid-flow delivery evidence, OPERATOR TEST, not customer activity (Base mainnet, 2026-11-15)
Request: POST https://aipaygen.com/v1/dns_lookup, body {"domain":"example.com"}, header `X-AIPayGen-Free: off` (free tier skipped).
1. Unpaid: HTTP 402, PAYMENT-REQUIRED quote 1000 atomic USDC on eip155:8453, payTo 0xebA22e8CD05Cb72A2F913099D6cCA666DD6D35B0.
2. Paid (same request + PAYMENT-SIGNATURE), 19:16:04 UTC: HTTP 200 with the DNS records, `receipt` {"payment":"x402","price":"$0.001","transaction":"0xfe3f2eadb4cf3e15cdfdc0780ae7150487acb89ae0b0edfccde42c325ae0433b","network":"eip155:8453"}, PAYMENT-RESPONSE {"success":true, same transaction}.
   Settlement: https://basescan.org/tx/0xfe3f2eadb4cf3e15cdfdc0780ae7150487acb89ae0b0edfccde42c325ae0433b (block 57898945, success, USDC 0x55c2…e617 → 0xebA2…35b0, 0.001).
3. Same signed payment resent: HTTP 200, same data, same transaction, `receipt.replay: true`, no second charge.
Earlier paid call the same way, 19:14:56 UTC: https://basescan.org/tx/0x76b1cb27022e62318b00b2daaf225426fe6251261a99e7979fd169c5c58620f8 (block 57898605, success).
Payer in all tests is the operator's own wallet 0x55c27e9b8e70a37af15f57b284be4dc9aa26e617. The signed payments are not published.

## Buyer guide
https://aipaygen.com/buyers. Summary:
- Call the tool; unpaid returns 402 with PAYMENT-REQUIRED. Sign with any x402 client and resend with PAYMENT-SIGNATURE.
- We verify, run the tool, and settle only if it succeeds, then return the result.
- Receipt: `receipt.transaction` in the body and the PAYMENT-RESPONSE header; check it on Basescan.

## Recovery when settlement or delivery is uncertain
- Tool fails: not settled, not charged; retry with the same signed payment.
- Settlement fails: 402 again, no result, nothing charged.
- Paid but the response was lost: resend the same request with the same PAYMENT-SIGNATURE within one hour; the same result and receipt come back (`receipt.replay: true`) with no new charge.
- The same payment sent twice at once: only one runs and settles; the other gets 409 PAYMENT_ALREADY_USED at no cost.
- Anything else: GitHub issues with the transaction hash.
- Private keys, usable signed payment authorizations and access tokens are not published.
