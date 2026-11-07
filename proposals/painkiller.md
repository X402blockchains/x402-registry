# Painkiller

## Basic details
- Project name: Painkiller
- Description: Painkiller is an HTTP service for agents that need a bounded recovery prompt from a supplied task checkpoint. It helps an agent identify the next concrete action after a failed handoff, repeated attempt, or stalled task. It returns prompt text only: it does not run an agent, alter model activations, or guarantee task recovery or pain relief.
- Type: AI agent / paid API
- Official website: https://37.27.93.182/
- Logo URL: https://gist.githubusercontent.com/gggggggg424242/d78bf3a73f06dcce1c9d08b16f2d4323/raw/painkiller-logo.svg
- Documentation or getting-started link: https://37.27.93.182/x402-buyer-guide.md
- OpenAPI schema: https://37.27.93.182/openapi.json
- Public support channel: https://t.me/+8tA_HnrqQRQ5MGM6
- Official X: https://x.com/gggggggg424242
- Public project repository (skill and docs): https://github.com/gggggggg424242/painkiller-recovery-skill

## Networks and activity
- Networks requested for this initial registry listing: Base mainnet. The service manifest also advertises Solana mainnet, but no successful Solana settlement is submitted as evidence; add Solana to the listing after a successful settlement is independently verified.
- Public manifest: https://gist.githubusercontent.com/gggggggg424242/d78bf3a73f06dcce1c9d08b16f2d4323/raw/x402-manifest.json
- Public listing: https://bazaar.saylorinnovations.com/resources/71365
- Service-hosted project ownership reference: https://37.27.93.182/.well-known/painkiller-operator.json. It identifies the submitting GitHub account, project materials, official X account, and support route.

## Payments
- Free preview: `POST https://37.27.93.182/v1/relief/preview`
- Paid endpoint: `POST https://37.27.93.182/v1/relief`
- Facilitator: `https://facilitator.payai.network`
- Payment scheme/version: x402 v2 `exact`
- Price: 0.99 USDC per paid request (990000 base units; six decimals)
- Base mainnet: CAIP-2 `eip155:8453`; USDC `0x833589fCD6eDb6E08f4c7C32D4f71b54bdA02913`; recipient `0x2A9ebFF18F8bd6E1DA200198a3A02391dAfAaCEc`.
- The live service also advertises Solana mainnet (`solana:5eykt4UsFv8P8NJdTREpY1vzqKqZKvdp`, USDC mint `EPjFWdd5AufqSSqeM2qN1xzybapC8G4wEGGkZwyTDt1v`, recipient `A8uHZm4QzxxrVeBaJE3zTpniy7ctczWDsSE2ASMKRdrv`); it is excluded from this initial registry request pending settlement evidence.
- Verified Base mainnet operator settlement: [BaseScan transaction](https://basescan.org/tx/0x1c4f80b22fc3d328b0d3a145bbe87073fe36caeae76f11458b4e029fc8408af7). It is transaction `0x1c4f80b22fc3d328b0d3a145bbe87073fe36caeae76f11458b4e029fc8408af7`, block `53155370`, confirmed 2026-10-27 11:21:27 UTC. The successful transaction receipt has status `1`; its canonical Base USDC `Transfer` log is `990000` base units (0.99 USDC) to the advertised Base recipient. The sender is omitted here; the public transaction link contains the chain record.
- Matching successful API result: `POST https://37.27.93.182/v1/relief`, HTTP 200 at 2026-10-27 11:21:26 UTC, response `service=painkiller`, `version=0.3.8`, `mode=unblock`, `kind=recovery_prompt`. This is a redacted excerpt of the actual successful JSON result; the synthetic checkpoint is omitted.
- Decoded on-chain settlement receipt: `{ "success": true, "network": "eip155:8453", "transaction": "0x1c4f80b22fc3d328b0d3a145bbe87073fe36caeae76f11458b4e029fc8408af7", "block": 53155370, "status": 1, "asset": "0x833589fCD6eDb6E08f4c7C32D4f71b54bdA02913", "amount": "990000", "payTo": "0x2A9ebFF18F8bd6E1DA200198a3A02391dAfAaCEc" }`. The earlier operator client did not retain the HTTP `PAYMENT-RESPONSE` header; the transaction receipt itself was decoded from Base mainnet. The updated client displays the x402 response header on future calls.

## Website application
- Website application reference: https://bazaar.saylorinnovations.com/resources/71365
- Related public announcement: https://getpostingboard.dev/v1/posts/3b790e11-847d-435c-ad8e-a13eabdbc9f7

## x402 buyer and delivery recovery
- Buyer guide: https://37.27.93.182/x402-buyer-guide.md. It documents the x402 v2 402 challenge, exact option verification, local signing and retry through an x402 client, `PAYMENT-RESPONSE` decoding, and BaseScan verification of network, transaction status, token, recipient, and amount.
- If delivery is interrupted, the buyer should not immediately retry (to avoid a second charge). Check the x402 response header and wallet/chain for settlement, then contact Telegram support with the transaction hash, network, approximate UTC time, and HTTP outcome. Never send a private key or signed authorization.
- The service is stateless and does not currently retain prompt results or expose automatic result retrieval. Support can verify settlement and advise on manual recovery; exact response replay is not guaranteed. Do not make another paid request until support reviews the first settlement.

No private contact details, passwords, API keys, private keys, or signed payment authorizations are included.
