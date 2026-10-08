# Solana Data API for AI agents

Status: public endpoint and logo checked; settlement evidence pending. This is a reviewed proposal, not a deployment or facilitator approval.

Application: https://github.com/X402blockchains/x402-registry/issues/2
Review date: 9 October 2026 (Asia/Kuala_Lumpur)

## Identity
- Type: paid API; not a facilitator.
- Website and documentation: https://solana-token-check.vercel.app/docs/
- Logo: https://solana-token-check.vercel.app/favicon.ico (HTTP 200; SVG)
- Public client repository: https://github.com/djubg/solana-data-api-x402
- Support: https://github.com/djubg/solana-data-api-x402/issues
- Manifest: https://solana-token-check.vercel.app/.well-known/x402
- Description: Pay-per-call token and wallet data for AI agents. The live manifest lists token checks, prices, trending/new tokens, reports, transactions, addresses and other resources.

## Verified unpaid discovery
GET https://solana-token-check.vercel.app/v1/trending returned HTTP 402 with a PAYMENT-REQUIRED header and x402Version 2 JSON. The scheme is exact. The challenge advertises both networks below, newer than the original Solana-only application.

| Network | Token | Atomic amount for checked endpoint | Payment recipient |
|---|---|---|---|
| Solana mainnet — solana:5eykt4UsFv8P8NJdTREpY1vzqKqZKvdp | USDC — EPjFWdd5AufqSSqeM2qN1xzybapC8G4wEGGkZwyTDt1v | 2000 (0.002 USDC at 6 decimals) | FG9LEt1suUtUv9eipkixS6DEWdSPVJkUjzjoDkL6UFU1 |
| Base mainnet — eip155:8453 | USDC — 0x833589fCD6eDb6E08f4c7C32D4f71b54bdA02913 | 2000 (0.002 USDC at 6 decimals) | 0xB2F01909D075b467965BEF7b0f1aF4Da46934573 |

The Solana challenge advertises feePayer CjNFTjvBhbJJd2B5ePPMHRLx1ELZpa8dwQgGL727eKww. This observation does not establish control of that address. PayAI is the facilitator claimed in the application; the unpaid challenge alone does not prove the settlement provider.

## Remaining before completed integration
- Applicant to confirm the current Base capability and provide a successful settlement receipt for each network being listed.
- No payment, paid response, historical count, volume or ownership signature was verified in this review.
- Register reviewed metadata in the production directory, refresh the deployment, and check the public page before closing the application.
- Do not manufacture transaction counts or mark this project as a facilitator.

