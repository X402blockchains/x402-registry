# Orivale Agent Intelligence

## Basic details
- Project name: Orivale Agent Intelligence
- What does it do? (2–3 sentences): Orivale Agent Intelligence provides keyless x402 v2 commercial APIs and a Dual-Rail Model Context Protocol (MCP) server for autonomous AI agents. Agents pay per call in USDC on Base to extract clean RAG Markdown, enrich B2B company domains, run frontier LLM inference, analyze Shopify competitors, and audit Base smart contracts with zero signup or API keys.
- Type: API / AI agent
- Official website: https://ori.mantissa.id/.well-known/x402
- Logo URL: https://ori.mantissa.id/favicon.svg
- Documentation or getting-started link: https://ori.mantissa.id/llms.txt (OpenAPI: https://ori.mantissa.id/openapi.json, Streamable HTTP MCP: https://ori.mantissa.id/mcp)
- Public support channel: https://github.com/tapirro/orivale-agent-mcp/issues

## Networks and activity
- Networks: Base mainnet (`eip155:8453`) only. This application is for Base only. (Our HTTP 402 responses also offer Solana `solana:5eykt4UsFv8P8NJdTREpY1vzqKqZKvdp`, but we have no settlements there yet, so we are not asking for Solana to be listed.)
- Public explorer or analytics link, if available: https://basescan.org/address/0xA7b5ae41563dFaA6E7DAfBE93cA2D650493A537B#tokentxns
- App contract/program or receiving addresses, with their networks, if available:
  - Base (`eip155:8453`): `0xA7b5ae41563dFaA6E7DAfBE93cA2D650493A537B`
- Proof that you represent the project (official website, repository or public announcement):
  - Domain discovery document `https://ori.mantissa.id/.well-known/x402` and `https://ori.mantissa.id/llms.txt` reference `https://github.com/tapirro/orivale-agent-mcp` and Base receiving address `0xA7b5ae41563dFaA6E7DAfBE93cA2D650493A537B`.
  - Official MCP Registry entry `io.github.tapirro/orivale-agent-mcp` (`https://registry.modelcontextprotocol.io/v0/servers?search=orivale`, published via GitHub Actions OIDC from `tapirro/orivale-agent-mcp`) points to `https://ori.mantissa.id/mcp` and `https://ori.mantissa.id/.well-known/x402`.

## Payments — only if your product accepts payments
- Paid endpoint and HTTP method:
  - `GET`/`POST` `https://ori.mantissa.id/v1/x402/bounties` (`$0.002` USDC)
  - `GET`/`POST` `https://ori.mantissa.id/v1/x402/clean-markdown` (`$0.001` USDC)
  - `GET`/`POST` `https://ori.mantissa.id/v1/x402/llm` (`$0.002` USDC)
  - `GET`/`POST` `https://ori.mantissa.id/v1/x402/b2b-enrich` (`$0.01` USDC)
  - `GET`/`POST` `https://ori.mantissa.id/v1/x402/shopify-competitor` (`$0.02` USDC)
  - `GET`/`POST` `https://ori.mantissa.id/v1/x402/contract-audit` (`$0.05` USDC)
- Facilitator used: PayAI Facilitator (`https://facilitator.payai.network`, all 6 endpoints indexed in PayAI Bazaar) + direct on-chain Base `txHash` verification
- Payment scheme/version: `exact` / x402 v2 (`x402Version: 2`)
- Token contract/mint and decimals:
  - Base USDC (`eip155:8453`): `0x833589fCD6eDb6E08f4c7C32D4f71b54bdA02913` (`6` decimals)
- Successful payment transaction link for each supported network:
  - Base mainnet (`0.002 USDC` settled from external payer): https://basescan.org/tx/0x3373a7e3513954c25a0aa66b84547cf7a13283fb132d70accb2ae09bb221f0e7
- Facilitator applicants: public supported/verify/settle URLs and signer/relayer addresses: Not applicable

## Website application
- Website application reference, if you have one: Not applicable
- Related issue or previous pull request, if any: None
