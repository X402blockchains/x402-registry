# Kronos BTC Price Forecast

## Basic details
- Project name: Kronos BTC Price Forecast
- What does it do? (2–3 sentences): Real-time Bitcoin (BTC) price forecasting API powered by the Kronos financial foundation model (transformer-based, trained for financial time series), running on live Coinbase matched-trade candles. Every paid call returns 12 predicted closes across a 60-minute horizon, tagged with the `method` ("kronos") that produced them so a caller can verify the model actually ran rather than serving cached/static data. A free preview endpoint lets buyers sample real output before paying.
- Type: API
- Official website: https://api.nexismvp.com
- Logo URL: none
- Documentation or getting-started link: https://api.nexismvp.com/openapi.json (OpenAPI spec with embedded x402 payment terms); free sample at https://api.nexismvp.com/forecast/btc/preview
- Public support channel: admin.online@nexismvp.com

## Networks and activity
- Networks: Base
- Public explorer or analytics link, if available: https://basescan.org/address/0x3B59f268EbC38c5F43B8B9bE37238bf43378Ad87
- App contract/program or receiving addresses, with their networks, if available: Base (eip155:8453) payee 0x3B59f268EbC38c5F43B8B9bE37238bf43378Ad87
- Proof that you represent the project: signed ownership attestation at https://api.nexismvp.com/.well-known/x402 — an EIP-191 personal-sign message confirming control of both the domain and the payee wallet, independently verifiable via `eth_account.Account.recover_message()` against the published signature (the recovered address matches the payee address above exactly).

## Payments — only if your product accepts payments
- Paid endpoint and HTTP method: GET /forecast/btc ($0.001 USDC, 1000 atomic units). Also GET /market/regime, GET /market/funding, GET /market/fear-greed, GET /market/gas-decision, POST /market/gas-preflight, POST /market/gas-audit, POST /market/pdf-to-markdown (same price, same facilitator) — 8 live products total on this domain.
- Facilitator used: Coinbase CDP (https://api.cdp.coinbase.com/platform/v2/x402)
- Payment scheme/version: x402 v2, exact
- Token contract/mint and decimals: USDC on Base, 0x833589fCD6eDb6E08f4c7C32D4f71b54bdA02913, 6 decimals
- Successful payment transaction link for each supported network: https://basescan.org/tx/0x07fba0c04f8e7cf16beb868956b47a62e37b33d42e82e0cc227e753e13346439 (Base mainnet, block 51592383) — a real third-party payment (not an operator test): payer 0x0fcbd49bf5faa1a132835e66ecf065bedd5a8774 paid 0.001 USDC to the payee address above for GET /forecast/btc.
- Facilitator applicants: Not applicable

## Website application
- Website application reference, if you have one: none
- Related issue or previous pull request, if any: none
