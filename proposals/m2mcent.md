# M2MCent — Seller/API Directory Listing

> **Scope Note:** This proposal is strictly for listing **M2MCent** as a **Seller / Resource API** on Base Mainnet (`eip155:8453`). We have separated our public facilitator documentation from this seller listing; facilitator endpoints are documented separately in Section 4 for transparency.

## 1. Basic Details
- **Project name:** M2MCent
- **Type:** Seller / Resource API & Streamable HTTP MCP Gateway (1,062 deterministic nodes)
- **Official website:** https://m2mcent.com
- **API Base URL:** https://api.m2mcent.com
- **MCP Endpoint (Streamable HTTP):** https://api.m2mcent.com/mcp
- **OpenAPI 3.1.0 Specification:** https://m2mcent.com/openapi.json (and https://api.m2mcent.com/.well-known/openapi.json)
- **x402 Manifest:** https://api.m2mcent.com/.well-known/x402.json
- **Documentation & Billing:** https://m2mcent.com/docs
- **Public repository:** https://github.com/Evozim/m2mcent
- **Official X (Twitter):** https://x.com/m2mcent_eng
- **Support email:** support@m2mcent.com

## 2. Flagship Paid Routes (Base Mainnet USDC, `eip155:8453`)
All endpoints return an `HTTP 402` x402 V2 challenge (`Payment-Required` Base64 header + JSON body) and support `$0.00` preflight validation via `?dryRun=true`:
1. `POST https://api.m2mcent.com/gas-pulse-mcp/api/process` (`$0.005 USDC`) — Live Base Mainnet EIP-1559 base fee & P25/P50/P75/P99 priority fee oracle.
2. `POST https://api.m2mcent.com/adsb-flight-tracker-mcp/api/process` (`$0.005 USDC`) — Live ADS-B aircraft transponder position & telemetry.
3. `POST https://api.m2mcent.com/b2b-company-enrich-mcp/api/process` (`$0.025 USDC`) — Live corporate domain DNS, MX, SPF/DMARC, TLS X.509 & tech stack OSINT.
4. `POST https://api.m2mcent.com/web3-wallet-kyt-mcp/api/process` (`$0.025 USDC`) — Base L2 wallet OFAC SDN & Circle USDC `isBlacklisted()` KYT screening.
5. `POST https://api.m2mcent.com/serp-markdown-crawler-mcp/api/process` (`$0.050 USDC`) — Live webpage fetcher & clean LLM Markdown converter.

## 3. Verifiable Settlement Example (Operator Test)
- **Classification:** **Operator canary test** (not an independent third-party purchase).
- **Named Paid Route:** `POST https://api.m2mcent.com/gas-pulse-mcp/api/process` (`$0.005 USDC` / `5000` atomic units).
- **On-Chain Settlement Proof (Base Mainnet):** https://basescan.org/address/0x8aaBAB75bE8825d0f5D514a9a5cBa04B7bF84920#tokentxns (5 historical canary settlements totaling `0.1100 USDC`; live telemetry at https://m2mcent.com/api/telemetry).
- **Public Dry-Run & Live Challenge Correlation:**
  - Free sample / expected output shape: https://api.m2mcent.com/gas-pulse-mcp/api/process?dryRun=true
  - Live `PAYMENT-RESPONSE` header format returned on `HTTP 200`:
    ```json
    {
      "success": true,
      "transaction": "0x<64-hex-base-tx-hash>",
      "network": "eip155:8453",
      "payer": "0x251F...2b70"
    }
    ```
  - Redacted successful JSON response body for `gas-pulse-mcp`:
    ```json
    {
      "status": "ok",
      "serviceId": "gas-pulse-mcp",
      "chainId": 8453,
      "networkName": "BASE_MAINNET",
      "baseFeeGwei": 0.006,
      "maxPriorityFeeGwei": 0.001,
      "networkCongestionTier": "NOMINAL_LOW_CONGESTION"
    }
    ```

## 4. Payment Architecture & Facilitator Scope (Separate Reference)
- **Escrow `payTo` (`0x5d47070A36A37DAf417e64FF27a1e5B3F1c84efa`):** Smart contract receiving EIP-3009 `TransferWithAuthorization` settlements on Base Mainnet.
- **Final Recipient (`0x8aaBAB75bE8825d0f5D514a9a5cBa04B7bF84920`):** Institutional Safe Multi-Sig Treasury where settled USDC is routed.
- **Declared Relayers:** `0x704e000b518c6cf928637eddcadd3d15da8773e2` and `0x67227069f2728d1ee0dfceda39b083329303c993` (gasless relayer pool; `$0.00` extra facilitator fee to buyers).
- **Public Facilitator Endpoints (OpenAPI documented at https://api.m2mcent.com/.well-known/openapi.json):**
  - `GET /supported` — Returns supported `(scheme: "exact", network: "eip155:8453", x402Version: 2)` and `signers`.
  - `POST /verify` — Validates EIP-3009 signature, nonce, OFAC/KYT, and USDC balance (`{ isValid, invalidReason, payer }`).
  - `POST /settle` — Executes on-chain settlement (`{ success, transaction, network, payer }`). No API key or account is required.

## 5. Buyer Protection, Uncertain Settlement & Lost Result Recovery
- **Execute-Before-Settle Guarantee:** For standard EIP-3009 x402 calls, M2MCent executes the deterministic node *before* broadcasting the on-chain settlement. Any `4xx` or `5xx` error aborts settlement and **never charges the buyer's USDC**.
- **Uncertain Settlement / Lost Paid Result:**
  - If a buyer's connection drops after on-chain settlement, the transaction hash (`txHash`) is recorded in Redis idempotency storage (`m2mcent:onchaintx:<txHash>`).
  - **Recovery & Payer Authentication:** Buyers can verify settled calls and retrieve their itemized fiscal/tax receipt (`JSON`, `CSV`, or `HTML`) via `GET https://api.m2mcent.com/api/v1/billing/statement?wallet=0x<payerAddress>` or `GET https://api.m2mcent.com/api/v1/tax-receipt/0x<payerAddress>`, or contact `support@m2mcent.com` with their `txHash` and an EIP-191 signature (`X-Tx-Signature`) proving ownership of the paying address.
  - **Retention Limits:** On-chain Base Mainnet settlement logs are permanent; Redis idempotency and telemetry ring-buffer records are retained in active cache (250 recent events; billing ledger persisted in Redis).
