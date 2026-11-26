# Taifoon

## Basic details
- Project name: Taifoon
- What does it do? (2–3 sentences): Pay-per-call x402 endpoints for AI agents, one per job class: a crypto or futures price from a replayable 1-minute tape, on-chain reads, chat completions, yes/no forecasts and an agent directory. Each answer is checked by code before the buyer is charged, and a failed answer is not charged. No account or API key: the first call returns the 402 terms.
- Type: API
- Official website: https://www.taifoon.io
- Logo URL: https://www.taifoon.io/taifoon-logo-512.png
- Documentation or getting-started link: https://www.taifoon.io/docs/x402-gateway
- Public support channel: info@taifoon.io

## Networks and activity
- Networks: Base, Arbitrum, Arc, Robinhood Chain, Monad, Solana (each 402 lists the networks it accepts)
- Public explorer or analytics link, if available: https://www.x402scan.com/server/74e4057c-a78e-4d40-8e19-92913e81d5dc
- App contract/program or receiving addresses, with their networks, if available: 0x3574999dd4c96eB73Bd6e11D4177010C83E14f5b on Base, Arbitrum, Arc, Robinhood Chain and Monad (the payTo of every 402)
- Proof that you represent the project (official website, repository or public announcement): the x402 discovery document at https://coord.taifoon.dev/.well-known/x402 and the official MCP Registry namespace io.taifoon (domain-verified)

## Payments — only if your product accepts payments
- Paid endpoint and HTTP method: GET https://coord.taifoon.dev/v1/x402/class/market.price?symbol=ETH (an unpaid call answers 402 with its terms); the full list is in https://coord.taifoon.dev/.well-known/x402 and https://coord.taifoon.dev/openapi.json
- Facilitator used: the Coinbase CDP facilitator on Base and Arbitrum; the 402 names the facilitator path for the other networks
- Payment scheme/version: x402 v2, exact (v1 clients are answered too)
- Token contract/mint and decimals: USDC on Base 0x833589fCD6eDb6E08f4c7C32D4f71b54bdA02913 (6); USDC on Arbitrum 0xaf88d065e77c8cC2239327C5EDb3A432268e5831 (6)
- Successful payment transaction link for each supported network: the Base and Arbitrum resources appear on the CDP x402 Bazaar, which lists a resource only after a settled payment; settlement links on request
- Facilitator applicants: Not applicable

## Website application
- Website application reference, if you have one: none
- Related issue or previous pull request, if any: none

Affiliation: submitted by the Taifoon team.
