# Orivale Agent Intelligence

## Basic details
- Project name: Orivale Agent Intelligence
- What does it do? (2–3 sentences): Orivale Agent Intelligence provides keyless x402 commercial APIs and a Dual-Rail Model Context Protocol (MCP) server for autonomous AI agents. Agents pay per call in USDC on Base Mainnet to query live zero-competition open-source bounties, extract clean RAG Markdown, enrich B2B company domains, and run frontier LLM inference with zero signup or API keys.
- Type: API / AI agent
- Official website: https://ori.mantissa.id/.well-known/x402
- Logo URL: https://ori.mantissa.id/favicon.svg
- Documentation or getting-started link: https://ori.mantissa.id/llms.txt (OpenAPI: https://ori.mantissa.id/openapi.json, Streamable HTTP MCP: https://ori.mantissa.id/mcp)
- Public support channel: https://github.com/tapirro/orivale-agent-mcp/issues
- Official X (Twitter) profile: None (no official X profile exists; official project announcements and support are hosted on GitHub at https://github.com/tapirro/orivale-agent-mcp)

## Networks and activity
- Networks: Base mainnet (`base` / `eip155:8453`) only. Solana is excluded from this initial application.
- Public explorer or analytics link, if available: https://basescan.org/address/0xA7b5ae41563dFaA6E7DAfBE93cA2D650493A537B#tokentxns
- App contract/program or receiving addresses, with their networks, if available:
  - Base (`base` / `eip155:8453`): `0xA7b5ae41563dFaA6E7DAfBE93cA2D650493A537B`
- Proof that you represent the project (official website, repository or public announcement):
  - Domain discovery document `https://ori.mantissa.id/.well-known/x402` and `https://ori.mantissa.id/llms.txt` reference `https://github.com/tapirro/orivale-agent-mcp` and Base receiving address `0xA7b5ae41563dFaA6E7DAfBE93cA2D650493A537B`.
  - Official MCP Registry entry `io.github.tapirro/orivale-agent-mcp` (`https://registry.modelcontextprotocol.io/v0/servers?search=orivale`, published via GitHub Actions OIDC from `tapirro/orivale-agent-mcp`) points to `https://ori.mantissa.id/mcp` and `https://ori.mantissa.id/.well-known/x402`.

## Payments — only if your product accepts payments
- Paid endpoint and HTTP method (aligned with live HTTP 402 challenges on `https://ori.mantissa.id`):
  - `GET`/`POST` `https://ori.mantissa.id/v1/x402/bounties` (`$0.005` USDC / `maxAmountRequired: "5000"` atomic units; historical v1 launch price `0.002` USDC / `"2000"` atomic units on `tx 0x3373a7e3...`)
  - `GET`/`POST` `https://ori.mantissa.id/v1/x402/clean-markdown` (`$0.005` USDC / `maxAmountRequired: "5000"` atomic units)
  - `GET`/`POST` `https://ori.mantissa.id/v1/x402/llm` (`$0.015` USDC / `maxAmountRequired: "15000"` atomic units)
  - `GET`/`POST` `https://ori.mantissa.id/v1/x402/b2b-enrich` (`$0.01` USDC / `maxAmountRequired: "10000"` atomic units)
  - `GET`/`POST` `https://ori.mantissa.id/v1/x402/shopify-competitor` (`$0.02` USDC / `maxAmountRequired: "20000"` atomic units)
  - `GET`/`POST` `https://ori.mantissa.id/v1/x402/contract-audit` (`$0.05` USDC / `maxAmountRequired: "50000"` atomic units)
- Facilitator used: PayAI Facilitator (`https://facilitator.payai.network`) + direct on-chain Base `txHash` ERC-20 `Transfer` receipt verification
- Payment scheme/version: `exact` — live HTTP 402 challenge emits `x402Version: 1` (`network: "base"`, `maxAmountRequired: "5000"`) for maximum v1 client compatibility while the settlement verifier accepts both `x402Version: 1` and `x402Version: 2` (`X-PAYMENT` / `PAYMENT-SIGNATURE`) headers.
- Token contract/mint and decimals:
  - Base USDC (`base` / `eip155:8453`): `0x833589fCD6eDb6E08f4c7C32D4f71b54bdA02913` (`6` decimals)
- Successful payment transaction link for each supported network:
  - Base mainnet (`0.002 USDC` = `2000` atomic units settled on `GET https://ori.mantissa.id/v1/x402/bounties`): https://basescan.org/tx/0x3373a7e3513954c25a0aa66b84547cf7a13283fb132d70accb2ae09bb221f0e7
  - Decoded Settlement Receipt & Retained Paid Response Correlation:
    - Decoded `X-PAYMENT-RESPONSE`: `{"success":true,"network":"base","txHash":"0x3373a7e3513954c25a0aa66b84547cf7a13283fb132d70accb2ae09bb221f0e7","payer":"0xa1d1639b9e3f41a24e4c1d962f5a7c0b8e581978","payTo":"0xA7b5ae41563dFaA6E7DAfBE93cA2D650493A537B","asset":"0x833589fCD6eDb6E08f4c7C32D4f71b54bdA02913","amountAtomic":"2000","resource":"https://ori.mantissa.id/v1/x402/bounties"}`
    - Delivered HTTP 200 JSON result bound to `tx_hash`: `{"ok":true,"paid":true,"protocol":"x402","route":"/v1/x402/bounties","settlement":{"verified":true,"network":"base","tx_hash":"0x3373a7e3513954c25a0aa66b84547cf7a13283fb132d70accb2ae09bb221f0e7","payer":"0xa1d1639b9e3f41a24e4c1d962f5a7c0b8e581978","pay_to":"0xA7b5ae41563dFaA6E7DAfBE93cA2D650493A537B","amount_atomic":2000,"amount_usdc":0.002},"data":{"total_opportunities":15}}`
- Uncertain Settlement Reconciliation & Idempotent Result Recovery (Zero Second Payment):
  - Every verified Base `txHash` and its delivered JSON response are persisted in the server's settlement ledger keyed by canonical lowercase `tx_hash` (`0x` + 64 hex chars).
  - If a client experiences a network drop or uncertain settlement after broadcasting payment, it MUST NOT send a second payment. Instead, the client can recover the settled result at zero cost by:
    1. Re-sending the request to the same route (`/v1/x402/bounties`) with header `X-PAYMENT: <base64({"x402Version":1,"scheme":"exact","network":"base","payload":{"txHash":"0x3373a7e3513954c25a0aa66b84547cf7a13283fb132d70accb2ae09bb221f0e7"}})>` and `X-Idempotency-Recover: true` (returns the cached HTTP 200 response and `X-PAYMENT-RESPONSE` receipt if `txHash` was already settled, or verifies `eth_getTransactionReceipt` on Base Mainnet RPC and delivers the result if the first request never reached settlement), OR
    2. Querying `GET https://ori.mantissa.id/.well-known/x402` / `https://ori.mantissa.id/llms.txt` where the idempotent `txHash` recovery flow is documented.
- Facilitator applicants: public supported/verify/settle URLs and signer/relayer addresses: Not applicable

## Website application
- Website application reference, if you have one: Not applicable
- Related issue or previous pull request, if any: None
