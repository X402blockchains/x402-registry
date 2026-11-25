# x402-contract-scan

## Basic details
- Project name: x402-contract-scan
- What does it do? (2–3 sentences): A pay-per-request risk scan API for EVM smart contracts. Send an address and get back a deterministic risk score, a verdict and the individual signals behind it, computed from live Base RPC data. Payment settles per request in USDC over x402, so there is no signup, API key or subscription.
- Type: API
- Official website: https://tim-scsi-treated-quite.trycloudflare.com
- Logo URL: https://github.com/quoze62.png
- Documentation or getting-started link: https://github.com/quoze62/x402-contract-scan
- Public support channel: https://github.com/quoze62/x402-contract-scan/issues

## Networks and activity
- Networks: Base
- Public explorer or analytics link, if available: https://basescan.org/address/0xd2DE5E9Db66Cd7720814dEF0f969BF2be90c1770
- App contract/program or receiving addresses, with their networks, if available: Base (eip155:8453) payee 0xd2DE5E9Db66Cd7720814dEF0f969BF2be90c1770
- Proof that you represent the project (official website, repository or public announcement): the live endpoint returns this same payTo address inside its 402 `accepts` payload, and the README plus source are published at https://github.com/quoze62/x402-contract-scan

## Payments — only if your product accepts payments
- Paid endpoint and HTTP method: GET https://tim-scsi-treated-quite.trycloudflare.com/v1/scan?address=0x... — HTTP 402 challenge with scheme `exact`, network `base`, asset `0x833589fCD6eDb6E08f4c7C32D4f71b54bdA02913` (USDC), maxAmountRequired 10000 (0.01 USDC), payTo 0xd2DE5E9Db66Cd7720814dEF0f969BF2be90c1770
- Facilitator: x402.org facilitator (https://x402.org/facilitator) via the x402-express middleware
- Free tier: GET https://tim-scsi-treated-quite.trycloudflare.com/v1/preview?address=0x... returns the risk score and verdict with no payment required.
