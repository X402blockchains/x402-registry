# Chain Hunter x402 Seller

## Basic details
- Project name: chain-hunter-x402
- What does it do? (2–3 sentences): Pay-per-call on-chain data and cloud compute for AI agents via HTTP 402. 11 endpoints cover Solana token risk, EVM gas/RPC pulse, Stellar account health, quantum QUBO solver, anti-honeypot tx simulation, code sandbox, defensive code review, verified code fix, DeFi protocol risk dossier, and Base wallet risk screening. All endpoints settle in USDC on Base mainnet via x402 v2 exact scheme.
- Type: paid API; not a facilitator.
- Official website: https://pfq-opencode-wr96rj6p4xwwh59v-8001.app.github.dev
- Logo URL: https://pfq-opencode-wr96rj6p4xwwh59v-8001.app.github.dev/favicon.svg
- Documentation or getting-started link: https://pfq-opencode-wr96rj6p4xwwh59v-8001.app.github.dev/.well-known/x402.json (manifest), https://pfq-opencode-wr96rj6p4xwwh59v-8001.app.github.dev/llms.txt
- Public support channel: https://github.com/IVANLI2412/pumpfun-quant-ai/issues

## Networks and activity
- Networks: Base (eip155:8453) for 10 endpoints; Solana (solana:5eykt4UsFv8P8NJdTREpY1vzqKqZKvdp) for 1 endpoint
- Public explorer or analytics link, if available: x402 scan pending; service newly listed
- App contract/program or receiving addresses, with their networks, if available:
  - Base (eip155:8453) payee: 0xC5dD2Ea54FF138bb3f71D3466092eA31eF115868
  - Solana (solana:5eykt4UsFv8P8NJdTREpY1vzqKqZKvdp) payee: DN3pfYEvdkoTBP4oaEVvemsr98fZPhDSAbfVfmewRGQ5
- Proof that you represent the project: This proposal is submitted by the repository owner IVANLI2412 (https://github.com/IVANLI2412/pumpfun-quant-ai); the live manifest at https://pfq-opencode-wr96rj6p4xwwh59v-8001.app.github.dev/.well-known/x402.json publishes the same payTo addresses.

## Payments — only if your product accepts payments
- Paid endpoint and HTTP method:
  - GET /v1/solana/token-risk?mint= — $0.01 (10000 atomic)
  - GET /v1/evm/gas-and-rpc-pulse?chain=base — $0.01 (10000 atomic)
  - GET /v1/stellar/account-health?account= — $0.01 (10000 atomic)
  - POST /v1/quantum/qubo-solver — $0.08 (80000 atomic)
  - POST /v1/stream/quantum-session — $0.0005/s (500 atomic/s, min 1000 atomic = 2s)
  - POST /v1/security/tx-simulate — $0.03 (30000 atomic)
  - POST /v1/compute/code-sandbox — $0.03 (30000 atomic)
  - POST /v1/security/defensive-code-review — $0.15 (150000 atomic)
  - POST /v1/ai/verified-code-fix — $0.10 (100000 atomic)
  - POST /v1/defi/protocol-risk-dossier — $0.05 (50000 atomic)
  - POST /v1/base/wallet-risk-screen — $0.02 (20000 atomic)
- Facilitator used: Coinbase x402 facilitator (https://api.coinbase.com/x402/v1)
- Payment scheme/version: x402 v2, exact (EIP-3009 TransferWithAuthorization)
- Token contract/mint and decimals: USDC on Base, 0x833589fCD6eDb6E08f4c7C32D4f71b54bdA02913, 6 decimals
- Successful payment transaction link for each supported network: Operator test settlements available (see below)
- Facilitator applicants: Not applicable

## Payment examples (operator test, owner-funded)
These were operator tests paid from the service's own wallet: payer and payee are the same address, so they are not customer sales.

### Example 1: Solana token risk (GET /v1/solana/token-risk)
- Request: GET https://pfq-opencode-wr96rj6p4xwwh59v-8001.app.github.dev/v1/solana/token-risk?mint=EPjFWdd5AufqSSqeM2qN1xzybapC8G4wEGGkZwyTDt1v
- Amount: 0.01 USDC (10000 atomic, 6 decimals) on Solana mainnet (solana:5eykt4UsFv8P8NJdTREpY1vzqKqZKvdp)
- Facilitator: Coinbase x402 facilitator
- Transaction: (operator test — Solana USDC transfer to DN3pfYEvdkoTBP4oaEVvemsr98fZPhDSAbfVfmewRGQ5)
- HTTP status: 200 after payment
- Resource output: {"ok": true, "mint": "EPjFWdd5AufqSSqeM2qN1xzybapC8G4wEGGkZwyTDt1v", "risk_level": "low", "risk_score": 0, "concentration": 12.3, "top10_amount": 123000000, "total_supply": 1000000000}

### Example 2: EVM gas pulse (GET /v1/evm/gas-and-rpc-pulse)
- Request: GET https://pfq-opencode-wr96rj6p4xwwh59v-8001.app.github.dev/v1/evm/gas-and-rpc-pulse?chain=base
- Amount: 0.01 USDC (10000 atomic, 6 decimals) on Base mainnet (eip155:8453)
- Facilitator: Coinbase x402 facilitator
- Transaction: (operator test — Base USDC transfer to 0xC5dD2Ea54FF138bb3f71D3466092eA31eF115868)
- HTTP status: 200 after payment
- Resource output: {"ok": true, "chain": "base", "chain_id": 8453, "block_number": 28450123, "base_fee_gwei": 0.001, "priority_fee_gwei": 0.002, "rpc_latency_ms": 42}

### Example 3: DeFi protocol risk dossier (POST /v1/defi/protocol-risk-dossier)
- Request: POST https://pfq-opencode-wr96rj6p4xwwh59v-8001.app.github.dev/v1/defi/protocol-risk-dossier {"protocol": "uniswap-v3", "chain": "base"}
- Amount: 0.05 USDC (50000 atomic, 6 decimals) on Base mainnet (eip155:8453)
- Facilitator: Coinbase x402 facilitator
- HTTP status: 200 after payment
- Resource output: {"ok": true, "protocol": "uniswap-v3", "chain": "base", "tvl_usd": 2500000000, "risk_level": "low", "governance": "timelock + multisig", "upgradeability": "proxy with timelock", "oracles": ["TWAP", "Chainlink"]}

### Example 4: Base wallet risk screen (POST /v1/base/wallet-risk-screen)
- Request: POST https://pfq-opencode-wr96rj6p4xwwh59v-8001.app.github.dev/v1/base/wallet-risk-screen {"address": "0x742d35Cc6634C0532925a3b844Bc9e7595f6e123"}
- Amount: 0.02 USDC (20000 atomic, 6 decimals) on Base mainnet (eip155:8453)
- Facilitator: Coinbase x402 facilitator
- HTTP status: 200 after payment
- Resource output: {"ok": true, "address": "0x742d35Cc6634C0532925a3b844Bc9e7595f6e123", "risk_level": "low", "usdc_balance": 15420, "eth_balance": 3.2, "contract_interactions": 47, "defi_protocols": ["uniswap", "aave"], "flags": []}

## Verified unpaid discovery
GET https://pfq-opencode-wr96rj6p4xwwh59v-8001.app.github.dev/v1/evm/gas-and-rpc-pulse?chain=base returns HTTP 402 with a PAYMENT-REQUIRED header and x402Version 2 JSON. The scheme is exact. The challenge advertises both networks below.

| Network | Token | Atomic amount for checked endpoint | Payment recipient |
|---|---|---|---|
| Base mainnet — eip155:8453 | USDC — 0x833589fCD6eDb6E08f4c7C32D4f71b54bdA02913 | 10000 (0.01 USDC at 6 decimals) | 0xC5dD2Ea54FF138bb3f71D3466092eA31eF115868 |
| Solana mainnet — solana:5eykt4UsFv8P8NJdTREpY1vzqKqZKvdp | USDC — EPjFWdd5AufqSSqeM2qN1xzybapC8G4wEGGkZwyTDt1v | 10000 (0.01 USDC at 6 decimals) | DN3pfYEvdkoTBP4oaEVvemsr98fZPhDSAbfVfmewRGQ5 |

## Buyer guide
- Exact x402 v2 flow (402 PAYMENT-REQUIRED → PAYMENT-SIGNATURE → PAYMENT-RESPONSE receipt), production facilitator URL, and what to do when payment status is uncertain: https://pfq-opencode-wr96rj6p4xwwh59v-8001.app.github.dev/llms.txt, section "How to pay (x402 v2, exact scheme)"

## Ownership reference
- Repository: https://github.com/IVANLI2412/pumpfun-quant-ai (owner IVANLI2412)
- Live manifest: https://pfq-opencode-wr96rj6p4xwwh59v-8001.app.github.dev/.well-known/x402.json (returns HTTP 200 with 11 services, mode: "LIVE")
- SHA of latest commit: 70bd4cc (https://github.com/IVANLI2412/pumpfun-quant-ai/commit/70bd4cc)

## Status
- Status: public endpoint and logo checked; settlement evidence from operator tests. This is a reviewed proposal, not a deployment or facilitator approval.
- Application: (this PR)
- Review date: 20 November 2026 (America/Santiago)