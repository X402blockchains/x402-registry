# Trading Signals Toolkit

## Basic details
- Project name: Trading Signals Toolkit
- What does it do? (2–3 sentences): Pay-per-call data API and remote MCP server for AI agents and traders. Its crypto routes return a safe/caution/avoid token verdict for Base and Solana tokens (mint/freeze authority, Token-2022 extensions, top-holder concentration, sniper/bundle wallets, liquidity and LP lock, live sell-route test), 24h whale flow (large DEX buys vs sells, net flow, top wallets), OFAC address screening and wallet pay-readiness. Agents pay per call in USDC over x402 with no signup or API key.
- Type: API (plus a remote MCP server)
- Official website: https://signals.incomefather.com
- Logo URL: https://signals.incomefather.com/favicon-32.png (social card: https://signals.incomefather.com/og-image.png)
- Documentation or getting-started link: https://signals.incomefather.com/llms.txt , https://signals.incomefather.com/openapi.json , https://signals.incomefather.com/guides/solana-token-safety-check-api , https://signals.incomefather.com/guides/crypto-whale-flow-api
- Public support channel: https://github.com/gdietsch/trading-signals-mcp/issues

## Networks and activity
- Networks: Base (eip155:8453), Solana mainnet (solana:5eykt4UsFv8P8NJdTREpY1vzqKqZKvdp)
- Public explorer or analytics link, if available: https://www.x402scan.com/ (listed), https://basescan.org/address/0x6d7be981c103eD360874a7703ad3CD6a98929aFB#tokentxns , https://solscan.io/account/BvE6kQthHmNPhegeSAA1qS5HvPG1DzngUuSVoLWdnQYV
- App contract/program or receiving addresses, with their networks, if available:
  - Base: 0x6d7be981c103eD360874a7703ad3CD6a98929aFB
  - Solana: BvE6kQthHmNPhegeSAA1qS5HvPG1DzngUuSVoLWdnQYV
- Proof that you represent the project (official website, repository or public announcement): this PR is opened by the owner of https://github.com/gdietsch/trading-signals-mcp , the MCP client package published to npm as trading-signals-mcp and to the MCP Registry as io.github.gdietsch/trading-signals-mcp, which points at https://signals.incomefather.com/mcp

## Payments — only if your product accepts payments
- Paid endpoint and HTTP method:
  - GET https://signals.incomefather.com/solana/token-verdict?mint=<mint> (0.01 USDC)
  - GET https://signals.incomefather.com/base/token-verdict?address=<address> (0.01 USDC)
  - GET https://signals.incomefather.com/crypto/whale-flow?token=<address or mint>&hours=24 (0.02 USDC)
  - GET https://signals.incomefather.com/bundle/token-pre-trade?token=<address or mint> (0.015 USDC)
  - Full route list: https://signals.incomefather.com/openapi.json
- Facilitator used: Coinbase CDP (Base) and PayAI (Base and Solana)
- Payment scheme/version: x402 v2, exact
- Token contract/mint and decimals: USDC on Base 0x833589fCD6eDb6E08f4c7C32D4f71b54bdA02913 (6 decimals); USDC on Solana EPjFWdd5AufqSSqeM2qN1xzybapC8G4wEGGkZwyTDt1v (6 decimals)
- Successful payment transaction link for each supported network: incoming settlements are visible on the receiving-address explorer pages above; specific transaction links can be provided on request.
- Facilitator applicants: Not applicable (not a facilitator)

## Website application
- Website application reference, if you have one: none
- Related issue or previous pull request, if any: none
