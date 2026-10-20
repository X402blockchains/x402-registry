# x402 Compliance Utilities

## Basic details
- Project name: x402 Compliance Utilities
- What does it do? (2–3 sentences): Two stateless, source-cited compliance data checks for AI agents, paid per call with x402. SAM.gov Registration Lookup returns selected public SAM.gov entity registration fields for a UEI at query time (legal name, CAGE, status, registration and expiration dates, exclusion flag). EUDR Lot Preflight checks the structure and basic formats of declared lot data against a dated EUDR Article 9 checklist; it is not a compliance determination.
- Type: API
- Official website: https://api.brightonhilyard.com
- Logo URL: Not yet available
- Documentation or getting-started link: https://api.brightonhilyard.com/openapi.json (OpenAPI 3.1)
- Public support channel: contact@brightonhilyard.com

## Networks and activity
- Networks: Base (eip155:8453), Solana (solana:5eykt4UsFv8P8NJdTREpY1vzqKqZKvdp)
- Public explorer or analytics link, if available: https://www.x402scan.com (registered as api.brightonhilyard.com)
- App contract/program or receiving addresses, with their networks, if available:
  - Base receiving address: 0xE3879e74EF899F8a8C0363955e6e17419DC7EDCF
  - Solana receiving address: EhY5bMYifPMGrxo2HDtE3MiKb9xwXLBrLKVUnWff6Y9P
- Proof that you represent the project (official website, repository or public announcement): The API is served from my own domain, brightonhilyard.com; the OpenAPI contact at https://api.brightonhilyard.com/openapi.json is contact@brightonhilyard.com.

## Payments — only if your product accepts payments
- Paid endpoint and HTTP method:
  - POST https://api.brightonhilyard.com/api/sam/registration ($0.05 USDC)
  - POST https://api.brightonhilyard.com/api/eudr/preflight ($0.50 USDC)
- Facilitator used: PayAI (https://facilitator.payai.network)
- Payment scheme/version: x402 v2, exact
- Token contract/mint and decimals:
  - Base USDC 0x833589fCD6eDb6E08f4c7C32D4f71b54bdA02913, 6 decimals
  - Solana USDC EPjFWdd5AufqSSqeM2qN1xzybapC8G4wEGGkZwyTDt1v, 6 decimals
- Successful payment transaction link for each supported network:
  - Solana: https://solscan.io/tx/FugvBHAzoQvE4kiGNBgde4Fm1oJ8k1uQTFyaXBRWVe2LU522LTmr1iVKCcXbnDdRuv4nyJVz1A6NooezXcHL1Pu (SAM.gov lookup, 0.05 USDC, 20 Oct 2026)
  - Base: no paid transaction yet; the endpoint returns a valid Base 402 offer.
- Facilitator applicants: public supported/verify/settle URLs and signer/relayer addresses: Not applicable

## Website application
- Website application reference, if you have one: Not applicable
- Related issue or previous pull request, if any: None

Do not include private contact details, passwords, API keys, private keys or signed payment authorizations.
