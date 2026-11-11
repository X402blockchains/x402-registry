# Moonbeam paid calls

## Basic details
- Project name: Moonbeam paid calls
- What does it do? (2–3 sentences): Paid calls for AI agents bought through Moonbeam: the latest BTC, ETH, SOL, NQ, ES or YM price, on-chain reads, a wallet address risk score and a text digest (sha256 or keccak256). Each answer is checked before the buyer is charged, and a failed answer is not charged. The same calls are served over plain HTTP with x402, MCP and A2A, with no account or API key.
- Type: API
- Official website: https://next.moonbeam.network/acp/plans
- Logo URL: https://next.moonbeam.network/icon.svg
- Documentation or getting-started link: https://next.moonbeam.network/acp/plans
- Public support channel: info@taifoon.io (the operator of these calls)

## Networks and activity
- Networks: Base, Arbitrum, Arc, Robinhood Chain, Monad, Solana (each 402 lists the networks it accepts)
- Public explorer or analytics link, if available: https://www.x402scan.com/server/1e570ff0-a889-44b3-ab3b-6bafcfa69d97
- App contract/program or receiving addresses, with their networks, if available: 0x3574999dd4c96eB73Bd6e11D4177010C83E14f5b on Base, Arbitrum, Arc, Robinhood Chain and Monad (the payTo of every 402)
- Proof that you represent the project (official website, repository or public announcement): the official MCP Registry entry network.moonbeam.next/paid-calls (the namespace is verified on the next.moonbeam.network domain) and the A2A card at https://next.moonbeam.network/.well-known/agent-card.json

## Payments — only if your product accepts payments
- Paid endpoint and HTTP method: GET https://next.moonbeam.network/api/acp/x402/class/market.price?symbol=ETH (an unpaid call answers 402 with its terms); MCP at https://next.moonbeam.network/api/acp/x402/mcp
- Facilitator used: the Coinbase CDP facilitator on Base and Arbitrum; the 402 names the facilitator path for the other networks
- Payment scheme/version: x402 v2, exact (v1 clients are answered too)
- Token contract/mint and decimals: USDC on Base 0x833589fCD6eDb6E08f4c7C32D4f71b54bdA02913 (6); USDC on Arbitrum 0xaf88d065e77c8cC2239327C5EDb3A432268e5831 (6)
- Successful payment transaction link for each supported network: none yet
- Facilitator applicants: Not applicable

## Website application
- Website application reference, if you have one: none
- Related issue or previous pull request, if any: none

Affiliation: submitted by Taifoon, which operates these calls for Moonbeam.
