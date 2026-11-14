# AIPayGen

## Basic details
- Project name: AIPayGen
- What does it do? (2–3 sentences): Pay-per-call tools for AI agents (web and company intelligence, AI text and media, crypto, markets and reference data), served over HTTP and a remote MCP server. Agents also search a free marketplace of 19,000+ APIs, MCP servers, skills and agents. Each paid tool is paid per call with x402 (no account), or with prepaid credits.
- Type: API (plus a remote MCP server)
- Official website: https://aipaygen.com
- Logo URL: https://aipaygen.com/logo.svg
- Documentation or getting-started link: https://aipaygen.com/llms.txt (OpenAPI: https://aipaygen.com/openapi.json; MCP: https://mcp.aipaygen.com/mcp; x402 resources: https://aipaygen.com/.well-known/x402)
- Public support channel: GitHub issues at https://github.com/Damien829/aipaygen/issues

## Networks and activity
- Networks: Base
- Public explorer or analytics link, if available: https://basescan.org/address/0xeba22e8cd05cb72a2f913099d6cca666dd6d35b0 (production receiving address). x402scan listing: https://www.x402scan.com (origin aipaygen.com, 146 resources registered 2026-11-14).
- App contract/program or receiving addresses, with their networks, if available: Base (eip155:8453) payee 0xeba22e8cd05cb72a2f913099d6cca666dd6d35b0 (current, production)
- Proof that you represent the project: see "Ownership reference" below.

## Payments — only if your product accepts payments
- Paid endpoint and HTTP method: GET or POST https://aipaygen.com/v1/{tool}, for 70 paid tools (for example POST https://aipaygen.com/v1/dns_lookup with {"domain": "example.com"}). Each tool's fixed USD price is in `x-payment-info` in the OpenAPI document and in the 402 quote. Free: https://aipaygen.com/v1/search_marketplace, docs, llms.txt.
- Facilitator used: Coinbase CDP (https://api.cdp.coinbase.com/platform/v2/x402)
- Payment scheme/version: x402 v2, exact (USDC transferWithAuthorization)
- Token contract/mint and decimals: USDC on Base, 0x833589fCD6eDb6E08f4c7C32D4f71b54bdA02913, 6 decimals
- Successful payment transaction link for each supported network: see "Payment example" below.
- Facilitator applicants: Not applicable to this application. AIPayGen also runs a facilitator (https://aipaygen.com/facilitator, setup guide https://aipaygen.com/merchants); a separate facilitator application will follow once it has settlements from its own signer.

## Website application
- Website application reference, if you have one: none
- Related issue or previous pull request, if any: none

## Payment example — OPERATOR TEST, not customer activity (Base mainnet)
- Request: an AIPayGen paid tool call, paid with x402
- Amount: 0.001 USDC (1000 atomic, 6 decimals) on Base mainnet (eip155:8453), 2026-11-14 12:52:56 UTC
- Payer: 0x55c27e9b8e70a37af15f57b284be4dc9aa26e617, the operator's own test wallet
- Transaction: https://basescan.org/tx/0x74d50969bc1748c2a6ca2ebd05c31fbdb9b686abf1cf6bd963a604996b7d9328 (block 57352002, status success; USDC Transfer 0x55c2…e617 → 0xeba2…35b0, 0.001 USDC; submitted by the CDP facilitator's relayer 0x93f6601151ccb08f333ab4b1cccfb1e188c0be44)
- This shows the production recipient and payment path work end to end; it is not presented as customer activity.

## Ownership reference
- This pull request is opened by GitHub account Damien829, which owns the source repository https://github.com/Damien829/aipaygen.
- The Official MCP Registry entry io.github.Damien829/aipaygen (GitHub-verified namespace, version 2.3.0) lists the remote https://mcp.aipaygen.com/mcp and website https://aipaygen.com.

## Buyer guide
- How to pay and call: https://aipaygen.com/llms.txt (section "Paying") and https://aipaygen.com/docs. An unpaid call returns an x402 v2 402 quote; sign it and resend with the PAYMENT-SIGNATURE header. Failed calls are never charged (payment settles only after the tool succeeds).

## Recovery and retained evidence
- A payment is settled only after the tool returns a result, so a failed call is not charged and can be retried with the same signed payment.
- Private keys, usable signed payment authorizations and access tokens are not published.
