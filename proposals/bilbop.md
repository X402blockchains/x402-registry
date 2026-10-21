# bilbop

- Type: API
- Description: Pay-per-call Solana tools for agents over x402 (USDC, no accounts): on-chain SPL mint info, token market brief, text summarize, Piper TTS WAV, and human brand feedback via WURK. Probe any POST unpaid for the 402 descriptor, settle USDC, retry.
- Website (HTTPS): https://bilbop-portfolio.pages.dev/
- Logo (HTTPS): https://bilbop-portfolio.pages.dev/bilbop-logo-512.png
- Documentation: https://api.bilbop.org/.well-known/x402 and https://api.bilbop.org/openapi.json
- Public repository: n/a (seller code private); public portfolio https://bilbop-portfolio.pages.dev/
- Networks and chain identifiers: Solana mainnet (`solana:5eykt4UsUbFJJapMLbpJBUhRc6GLyZFYFvBcwfZoE4j4`)
- Paid resource URLs and HTTP methods:
  - POST https://api.bilbop.org/v1/summarize
  - POST https://api.bilbop.org/v1/sol-token-brief
  - POST https://api.bilbop.org/v1/sol-mint-info
  - POST https://api.bilbop.org/v1/tts
  - POST https://api.bilbop.org/brand-feedback
- x402 version and payment scheme: x402 v2, exact
- Token contract or mint, decimals: USDC `EPjFWdd5AufqSSqeM2qN1xzybapC8G4wEGGkZwyTDt1v`, 6 decimals
- Seller payment recipient addresses: `2r2vsoyuYuy4dsyQVRhfmMBqsMRKHRS5FTPNumYFhxE4` (Solana)
- Facilitator URL and supported endpoint: PayAI facilitator (Solana USDC exact); also indexed via Coinbase CDP Bazaar
- Facilitator signer / relayer addresses (if applicable): PayAI fee-payer `CjNFTjvBhbJJd2B5ePPMHRLx1ELZpa8dwQgGL727eKww` (observed on settles)
- Example successful settlement hashes and explorer links:
  - https://solscan.io/tx/3nAddg7gUCp4SD5QpCN2tQqjyvhPebWWYn43uczd2vRctAW4igLjfambVwnKzpZskfm6htbkCQz6hq2nRxtGv7ZS (2026-09-29, +0.01 USDC to seller)
- Ownership evidence (domain-hosted proof or public project reference): Permanent front door https://api.bilbop.org (Cloudflare Worker custom domain on bilbop.org); portfolio https://bilbop-portfolio.pages.dev/; 402index verified claim for api.bilbop.org
- Public support channel: watchdogsfreak@gmail.com

Disclosure: this proposal is submitted by the bilbop operator (affiliation: we run this service).
