# YRUZ

- Type: API (seller; not a facilitator)
- Description: Pay-per-call APIs for AI agents over x402 v1 and v2, no account or API key. Crypto tools (/api/crypto): live prices for up to 25 coins or Solana mints per call ($0.002), trending coins with top gainers and losers ($0.003), a Solana token rug-pull check with mint/freeze authority, holder concentration, liquidity and a 0-100 risk score ($0.005), Solana wallet portfolio in USD ($0.005), Solana transaction decoding ($0.003) and current Solana priority fees and Base gas ($0.002). Agent tools: web page to Markdown (/api/extract, $0.005), link unfurl ($0.003), domain intel with DNS, SPF, DMARC, DKIM, RDAP and TLS ($0.01), broken-link check ($0.01), x402 endpoint validation ($0.005), uptime with timings ($0.003), USDC wallet balance ($0.002) and a scored website audit ($0.01). Also public social data from the YRUZ network, 18 developer utilities and a 90+ tool toolkit with 1,700+ converters. 269 paid operations. Invalid or private input is refused with a free 400 before payment.
- Website (HTTPS): https://yruz.one
- Logo (HTTPS): https://yruz.one/content/themes/yruz/images/favicon.png
- Documentation: https://yruz.one/llms.txt (also https://yruz.one/auth.md and https://yruz.one/x402.php)
- Public repository: https://github.com/xzntexe/yruz-x402 (public catalogue, OpenAPI and client examples; the service source is closed). Machine-readable contracts: https://yruz.one/openapi.json, https://yruz.one/.well-known/x402, https://yruz.one/.well-known/apis.json
- Networks and chain identifiers: Solana mainnet (solana:5eykt4UsFv8P8NJdTREpY1vzqKqZKvdp) and Base mainnet (eip155:8453). Every 402 offers the same price on both.
- Paid resource URLs and HTTP methods: the live list is at https://yruz.one/.well-known/x402 (141 resources); every resource accepts GET with query parameters and POST with a JSON body (https://yruz.one/openapi.json, 269 operations with x-payment-info). Host: yruz.one only.
- x402 version and payment scheme: x402 v2 (PAYMENT-REQUIRED header, PAYMENT-SIGNATURE) and x402 v1 (JSON body, X-PAYMENT), scheme exact
- Token contract or mint, decimals: USDC on Solana EPjFWdd5AufqSSqeM2qN1xzybapC8G4wEGGkZwyTDt1v, 6 decimals; USDC on Base 0x833589fCD6eDb6E08f4c7C32D4f71b54bdA02913, 6 decimals (EIP-712 domain "USD Coin" / "2")
- Seller payment recipient addresses: Solana CWfaj5vDppWCp4q1X4iPYGWpCGY2Rerj9DQWqxTnz1Pp; Base 0x235b73D50752800D9FaE24F51bEb08f47076c67A
- Facilitator URL and supported endpoint (we are not the facilitator):

  | | OpenFacilitator | PayAI | Dexter |
  |---|---|---|---|
  | Base URL | `https://pay.openfacilitator.io` | `https://facilitator.payai.network` | `https://x402.dexter.cash` |
  | Supported | `GET https://pay.openfacilitator.io/supported` | `GET https://facilitator.payai.network/supported` | `GET https://x402.dexter.cash/supported` |
  | Verify / Settle | `POST /verify`, `POST /settle` | `POST /verify`, `POST /settle` | `POST /verify`, `POST /settle` |
  | Auth | none | none for `exact` | none |
- Facilitator signer / fee payer addresses (not YRUZ addresses): Solana fee payers as offered in our 402: OpenFacilitator Hbe1vdFs4EQVVAzcV12muHhr6DEKwrT9roMXGPLxLBLP, PayAI CjNFTjvBhbJJd2B5ePPMHRLx1ELZpa8dwQgGL727eKww, Dexter DeXterR2kQm8AvRHnNPatWkE46TfAcMeBDjb6FySoAb8.
- Example successful settlement hashes (customer payments for GET https://yruz.one/api/audit, 0.01 USDC each, Base):
  - https://basescan.org/tx/0xe95e08567b9aa918f69fbaa99006cdb9d26ff51c5325b2f6f83c4ed841a4ff1f (2026-10-20, via OpenFacilitator)
  - https://basescan.org/tx/0xedefc1a77c72e5b5e91f922259e93d15948e0d3d3864257925537d8f6db2b535 (2026-10-20, via PayAI)
- Ownership evidence: both payTo addresses appear in the unpaid 402 challenge served by yruz.one (e.g. `curl -i https://yruz.one/api/crypto/price`); the same addresses are in https://yruz.one/.well-known/x402 and https://yruz.one/openapi.json (x-x402.accepts). Domain verification is also live on 402index.io and agent-tools.cloud.
- Public support channel: zanto@yruz.one
