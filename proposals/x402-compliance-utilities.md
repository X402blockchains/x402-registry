# x402 Compliance Utilities

## Basic details
- Project name: x402 Compliance Utilities
- What does it do? (2–3 sentences): Two stateless, source-cited compliance data checks for AI agents, paid per call with x402. SAM.gov Registration Lookup returns selected public SAM.gov entity registration fields for a UEI at query time (legal name, CAGE, status, registration and expiration dates, exclusion flag). EUDR Lot Preflight checks the structure and basic formats of declared lot data against a dated EUDR Article 9 checklist. It is a structural check only, not a compliance determination.
- Type: API
- Official website: https://api.brightonhilyard.com
- Logo URL: https://api.brightonhilyard.com/logo.png (512×512 PNG; SVG at https://api.brightonhilyard.com/logo.svg)
- Documentation or getting-started link: https://api.brightonhilyard.com/openapi.json (OpenAPI 3.1)
- Public support channel: contact@brightonhilyard.com

## Networks and activity
- Networks: Base (eip155:8453), Solana (solana:5eykt4UsFv8P8NJdTREpY1vzqKqZKvdp)
- Public explorer or analytics link, if available: https://www.x402scan.com (registered as api.brightonhilyard.com)
- App contract/program or receiving addresses, with their networks, if available:
  - Base receiving address: 0xE3879e74EF899F8a8C0363955e6e17419DC7EDCF
  - Solana receiving address: EhY5bMYifPMGrxo2HDtE3MiKb9xwXLBrLKVUnWff6Y9P
- Proof that you represent the project (official website, repository or public announcement): The API is served from my own domain, brightonhilyard.com. The OpenAPI contact at https://api.brightonhilyard.com/openapi.json is contact@brightonhilyard.com.

## Payments — only if your product accepts payments
- Paid endpoint and HTTP method:
  - POST https://api.brightonhilyard.com/api/sam/registration ($0.05 USDC)
  - POST https://api.brightonhilyard.com/api/eudr/preflight ($0.50 USDC)
- Facilitator used: Coinbase CDP facilitator (https://api.cdp.coinbase.com/platform/v2/x402). The first Solana payment below was settled through PayAI before the switch.
- Payment scheme/version: x402 v2, exact
- Token contract/mint and decimals:
  - Base USDC 0x833589fCD6eDb6E08f4c7C32D4f71b54bdA02913, 6 decimals
  - Solana USDC EPjFWdd5AufqSSqeM2qN1xzybapC8G4wEGGkZwyTDt1v, 6 decimals
- Successful payment transaction link for each supported network:
  - **Base:** https://basescan.org/tx/0xb76545f511d33b0ffeac235eb05a9b8ba4772a0b8944b572dc3ce8c2dadcfc8e (POST /api/sam/registration, 0.05 USDC, 21 Oct 2026 19:31 UTC, CDP facilitator)
  - **Solana:** https://solscan.io/tx/4YgjnRypbgsf9PNNPczp6hyHBsjk38Wbjf2qbkf9HMta7jts4ACgEX3xobNrcWK3uL2XJMPMTqAB6e9BFdMnC4W2 (POST /api/sam/registration, 0.05 USDC, 20 Oct 2026 22:51 UTC, CDP facilitator)
  - Solana (earlier, PayAI, already verified): https://solscan.io/tx/FugvBHAzoQvE4kiGNBgde4Fm1oJ8k1uQTFyaXBRWVe2LU522LTmr1iVKCcXbnDdRuv4nyJVz1A6NooezXcHL1Pu
- Facilitator applicants: public supported/verify/settle URLs and signer/relayer addresses: Not applicable

### Payment example with response and receipt (Base)

Request (after the 402 challenge, retried with a `PAYMENT-SIGNATURE` header; the signed payload is omitted):

```http
POST /api/sam/registration HTTP/1.1
Host: api.brightonhilyard.com
Content-Type: application/json
PAYMENT-SIGNATURE: <base64 x402 v2 payment payload, omitted>

{"uei":"G4KDGE4JFFK7"}
```

Accepted requirement it paid against (from the decoded `PAYMENT-REQUIRED` header):

```json
{ "scheme": "exact", "network": "eip155:8453", "amount": "50000",
  "asset": "0x833589fCD6eDb6E08f4c7C32D4f71b54bdA02913",
  "payTo": "0xE3879e74EF899F8a8C0363955e6e17419DC7EDCF", "maxTimeoutSeconds": 300 }
```

Response: `HTTP/1.1 200 OK`. The body is public SAM.gov registration data for a large federal contractor, so nothing needs redacting:

```json
{"service":"sam-registration-status","result":"found","uei":"G4KDGE4JFFK7",
 "legalBusinessName":"LOCKHEED MARTIN CORPORATION","cageCode":"81755","registrationStatus":"Active",
 "registrationDate":"2002-03-26","registrationExpirationDate":"2027-06-15","exclusionStatusFlag":"N",
 "source":"SAM.gov Entity Management API","checkedAt":"2026-10-21T19:31:05.614Z",
 "note":"Public SAM.gov registration data at query time; not a certification, sanctions check, identity check, or general trust assessment."}
```

Decoded `PAYMENT-RESPONSE` settlement receipt for the same call:

```json
{ "success": true,
  "payer": "0x771C7f05BFB810A969B38276D4Bcd7AdaB6f7412",
  "transaction": "0xb76545f511d33b0ffeac235eb05a9b8ba4772a0b8944b572dc3ce8c2dadcfc8e",
  "network": "eip155:8453" }
```

The Solana CDP payment returned the same body (`checkedAt` 2026-10-20T22:51:33.772Z) with the receipt `{"success":true,"payer":"BV9jZLyK2Xm4pFJBgk3mkMoJrQvyKEJxqkHxsqyQTZde","transaction":"4YgjnRypbgsf9PNNPczp6hyHBsjk38Wbjf2qbkf9HMta7jts4ACgEX3xobNrcWK3uL2XJMPMTqAB6e9BFdMnC4W2","network":"solana:5eykt4UsFv8P8NJdTREpY1vzqKqZKvdp"}`.

### Buyer instructions

1. **Challenge.** Send the POST with a JSON body and no payment header. The server answers `402` with a `PAYMENT-REQUIRED` header: base64 JSON, `x402Version: 2`, and an `accepts[]` list offering `exact` USDC on Base and Solana, with the price, asset, `payTo` and `maxTimeoutSeconds: 300`. Solana offers include the facilitator `feePayer`, so buyers need no SOL. Base payments use a gasless EIP-3009 authorization, so buyers need no ETH.
2. **Pay.** Choose one offer and sign an x402 v2 `exact` payment for exactly that offer (Base: EIP-3009 `transferWithAuthorization`; Solana: a partially signed USDC `TransferChecked` with the facilitator as fee payer). Resend the same request and body with the base64 payload in the `PAYMENT-SIGNATURE` header. v1 clients may use `X-PAYMENT`. Any x402 v2 client works, for example `@x402/fetch` (`wrapFetchWithPayment`).
3. **Receipt.** On success you get `200` with the JSON result and a `PAYMENT-RESPONSE` header: base64 JSON `{ success, payer, transaction, network }`. Keep it as your receipt. The transaction is visible on Basescan or Solscan.
4. **Failures are not charged.** Settlement happens only after the handler succeeds. A `4xx`/`5xx` from the service (invalid UEI, SAM.gov unavailable or quota reached) means the payment was not settled. A `402` returned on the paid retry means the payment was rejected and nothing was charged.
5. **Timeouts and uncertain payments.** If the connection drops after you send `PAYMENT-SIGNATURE`:
   - Retry with the **same** request and the **same** `PAYMENT-SIGNATURE`. A given authorization can settle at most once: a Base EIP-3009 nonce and a Solana transaction signature cannot be replayed.
   - Do **not** sign a new payment until you have confirmed on-chain that the first did not settle and has expired. On Base, check for a USDC transfer from your address to `payTo` for the amount, or call `authorizationState(you, nonce)` on the USDC contract; the authorization expires after `maxTimeoutSeconds` (300 s). On Solana, look up the transaction signature from your signed payload; it expires with its blockhash, about 1–2 minutes.
   - If a payment settled but you did not receive the result, email contact@brightonhilyard.com with the transaction link for manual resolution.

## Website application
- Website application reference, if you have one: Not applicable
- Related issue or previous pull request, if any: This PR (#17)

Do not include private contact details, passwords, API keys, private keys or signed payment authorizations.
