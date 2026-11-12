# Horizon Pulse
- Type: API (seller; not a facilitator)
- Description: Pay-per-call APIs over x402, no API key: web search, web fetch to markdown, HTTP proxy, structured page extract, PDF to text, x402 endpoint checks, SEC/BLS/Treasury data, domain checks, NWS weather, a website audit and an agent-readiness report, across 58 paid HTTP resources (unique paid URLs listed at https://horizonpulse.dev/.well-known/x402, including 2 Base-only premium tiers; 65 paid OpenAPI operations, since some URLs accept GET and POST; 3 free routes are not counted). Also a remote MCP server at https://horizonpulse.dev/mcp (56 tools from tools/list: 30 paid, 23 that only return a route's payment terms without charging, and 3 free). Payments in USDC on Base for all 58 resources and on Solana for 28 of them; the 402 may also list Polygon, XRPL and EURC entries, which are not part of this listing.
- Website (HTTPS): https://horizonpulse.dev
- Logo (HTTPS): https://horizonpulse.dev/icon.png
- Documentation: https://horizonpulse.dev/llms.txt
- Networks and chain identifiers: HTTP API: Base mainnet (eip155:8453, via Coinbase CDP) and Solana mainnet (solana:5eykt4UsFv8P8NJdTREpY1vzqKqZKvdp, via PayAI); the 402 may also list XRPL and Polygon entries, which are not part of this listing. Hosted MCP (https://horizonpulse.dev/mcp) and the local MCP client: Base only (eip155:8453).
- Paid resource URLs and HTTP methods: the live list, with methods, is at https://horizonpulse.dev/.well-known/x402 (host: horizonpulse.dev only)
- x402 version and payment scheme: x402 v2, exact
- Token contract or mint, decimals: USDC on Base 0x833589fCD6eDb6E08f4c7C32D4f71b54bdA02913, 6 decimals; USDC on Solana EPjFWdd5AufqSSqeM2qN1xzybapC8G4wEGGkZwyTDt1v, 6 decimals
- Seller payment recipient addresses: Base 0x5b32c973596078a967562ca652761404f19be0e9; Solana BjY98A6dS3GGLZdz2zHy8wK7XAwnQgNhCc66mfmBTRPz
- Facilitator URL and supported endpoint (we are not the facilitator):

  | | Coinbase CDP (Base) | PayAI (Solana) |
  |---|---|---|
  | Base URL | `https://api.cdp.coinbase.com/platform/v2/x402` | `https://facilitator.payai.network` |
  | Supported | `GET https://api.cdp.coinbase.com/platform/v2/x402/supported` | `GET https://facilitator.payai.network/supported` |
  | Verify | `POST https://api.cdp.coinbase.com/platform/v2/x402/verify` | `POST https://facilitator.payai.network/verify` |
  | Settle | `POST https://api.cdp.coinbase.com/platform/v2/x402/settle` | `POST https://facilitator.payai.network/settle` |
  | Auth | CDP API key (Bearer JWT); 401 without it | none for `exact`; GET endpoints public |
- Facilitator signer / relayer addresses (not Horizon Pulse addresses; listed separately from the payTo addresses above): PayAI Solana fee payer CjNFTjvBhbJJd2B5ePPMHRLx1ELZpa8dwQgGL727eKww (in PayAI /supported signers["solana:*"]). Base: the 2026-10-13 test transaction was submitted on-chain by 0x97acce27d5069544480bde0f04d9f47d7422a016 (facilitator-side sender; not a Horizon Pulse address).
- Example successful settlement hashes and explorer links (operator test payments, not customer activity; GET https://horizonpulse.dev/api/pulse, 0.005 USDC each, 2026-10-13):
  - Base: https://basescan.org/tx/0xe0fdf8231544f4da2162f8b4c2eb1299f338ab88486096ba54b77d7ac5cfbcd5 (block 52553538)
  - Solana: https://solscan.io/tx/2hUu7qauJuEXcLfzYnXZ7p4berVA49Mvd9hmtkWWRznsFQg9oWNMP1zfU1RrENTaTNLUX13oNm6gioKhFwokA1p7 (slot 456450921)
- Ownership evidence (domain-hosted proof or public project reference): https://horizonpulse.dev is the official website. Its header and footer link the project's X account, https://x.com/HorizonPulseAPI, and its footer and https://horizonpulse.dev/llms.txt publish the contact address horizonpulse.co@proton.me. Both payTo addresses listed above appear in the unpaid 402 challenge served by horizonpulse.dev. This PR is opened from the horizon-pulse GitHub account.
- Public support channel: horizonpulse.co@proton.me (published at https://horizonpulse.dev/llms.txt) or https://x.com/HorizonPulseAPI
