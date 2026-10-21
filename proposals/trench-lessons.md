# Trench Lessons
- Type: API (paid x402 seller); not a facilitator.
- Description: Solana meme coin research API for trading bots. Pay-per-request daily findings feed (pump.fun / PumpSwap / Meteora, with sources) and per-mint pre-trade risk flags (curveSkipPool, unlockedLp, mayhemMode, bundleHandoff, each with status and confidence). Research only, not financial advice.
- Website (HTTPS): https://trench-lessons.vercel.app
- Logo (HTTPS): https://trench-lessons.vercel.app/logo.png (HTTP 200, image/png)
- Documentation: buyer payment guide in "Buyer payment guide" below (prices, headers, receipts, timeouts and safe retry) · https://trench-lessons.vercel.app/api-docs · https://trench-lessons.vercel.app/llms.txt · https://trench-lessons.vercel.app/openapi.json · https://trench-lessons.vercel.app/.well-known/x402
- Public repository: none published yet.
- Networks and chain identifiers: Solana mainnet only, solana:5eykt4UsFv8P8NJdTREpY1vzqKqZKvdp.
- Paid resource URLs and HTTP methods (GET only; an unpaid GET returns the 402 terms and is never charged):
  - GET https://trench-lessons.vercel.app/api/signals/risk/{mint}: 10000 atomic USDC (0.01 USDC). `{mint}` is any base58 SPL mint (32–44 chars). Free unpaid sample: /api/signals/risk/sample.
  - GET https://trench-lessons.vercel.app/api/lessons/feed?days=1..30: 5000 atomic USDC (0.005 USDC). `days` defaults to 7.
- x402 version and payment scheme: x402 v2, scheme exact (SVM). Bazaar discovery extension on every 402. `maxTimeoutSeconds` (300 s) is the seller's settlement time limit, not the signature expiry; a signed Solana payment is only valid while its recent blockhash is valid (roughly 60–90 s).
- Token contract or mint, decimals: USDC, EPjFWdd5AufqSSqeM2qN1xzybapC8G4wEGGkZwyTDt1v, 6 decimals.
- Seller payment recipient addresses: 7JAuWxcEpZL2wK3gm6eTR2p7d1SAofM4EHxuTgemAAae (USDC token account D4CwjiE8uu3SqJfAU9sBb1ogDyHJAmbxj4r4HiKAMN5j).
- Scope: seller-only listing; Trench Lessons does not offer facilitator endpoints to third parties.
- Facilitator URL and supported endpoint: PayAI, https://facilitator.payai.network (`/supported`, `/verify`, `/settle`). Free tier, no buyer credentials. No fallback facilitator: if PayAI fails, the call is not settled.
- Settlement order: verify → run the handler → settle only if the handler answered < 400 → return the data with PAYMENT-RESPONSE (`@x402/next` 2.28 `withX402`). Handler errors are not settled.
- Facilitator signer / relayer addresses (if applicable): PayAI fee payer CjNFTjvBhbJJd2B5ePPMHRLx1ELZpa8dwQgGL727eKww (advertised in `accepts[].extra.feePayer`; fee payer of every settlement below). Not a Trench Lessons address.
- Example successful settlement hashes and explorer links: see "Settlement evidence" below.
- Ownership evidence (domain-hosted proof or public project reference): the payTo above is published in the live 402 challenges served by trench-lessons.vercel.app, in https://trench-lessons.vercel.app/.well-known/x402 and in https://trench-lessons.vercel.app/api/pricing. On-chain, the test payer below was funded by the payTo itself (tx 5VNzUMZToGV4Ge2iowjonCWm8nK3Ae2MqSBawL49NtYnEaXD6pskFBzsGyEHksPYswqb8TPF3bBps2FHJuqG7zot, 0.03 USDC from payTo to the test wallet).
- Public support channel: https://x.com/ProfitzDigital

## Buyer payment guide

### 1. Catalogue and prices

| Method | URL | Price (atomic USDC / USDC) | Notes |
|---|---|---|---|
| GET | `https://trench-lessons.vercel.app/api/signals/risk/{mint}` | 10000 / 0.01 | Risk flags with `value`, `status` (ok / unknown / n/a), `confidence`; `riskScore` 0–100 |
| GET | `https://trench-lessons.vercel.app/api/lessons/feed?days=N` | 5000 / 0.005 | N = 1..30 most recent daily lessons |

Machine-readable: `/.well-known/x402`, `/openapi.json`, and the Bazaar `extensions.bazaar` block (input/output schema) in each 402.

### 2. Request flow and headers (checked live on 2026-10-18 15:14 UTC)

1. Send the GET with no payment header. The server answers `402` with:
   - `PAYMENT-REQUIRED`: base64 JSON, `x402Version: 2`, `resource`, and one `accepts` entry: `{"scheme":"exact","network":"solana:5eykt4UsFv8P8NJdTREpY1vzqKqZKvdp","amount":"10000"|"5000","asset":"EPjFWdd5AufqSSqeM2qN1xzybapC8G4wEGGkZwyTDt1v","payTo":"7JAuWxcEpZL2wK3gm6eTR2p7d1SAofM4EHxuTgemAAae","maxTimeoutSeconds":300,"extra":{"feePayer":"CjNFTjvBhbJJd2B5ePPMHRLx1ELZpa8dwQgGL727eKww"}}`.
   - The same object as the JSON body (for clients that read only the body), plus `Cache-Control: no-store`.
2. Build an exact SVM payment: a USDC `TransferChecked` from your token account to the payTo's USDC account for exactly `amount`, with PayAI's `feePayer` as fee payer, partially signed by you. Retry the same GET with header `PAYMENT-SIGNATURE: <base64 payment payload>`. Standard clients (`@x402/fetch` + `@x402/svm` `ExactSvmScheme`) do this automatically.
3. On success: `200`, JSON body, and `PAYMENT-RESPONSE` (base64 JSON): `{"success":true,"payer":"<your address>","transaction":"<Solana signature>","network":"solana:5eykt4UsFv8P8NJdTREpY1vzqKqZKvdp"}`.

### 3. Receipts

The decoded `PAYMENT-RESPONSE.transaction` is the Solana signature of your settlement; check it at `https://solscan.io/tx/<signature>` or with RPC `getTransaction`. A valid receipt is a finalized transaction with `err: null` and a `TransferChecked` of `amount` USDC into `D4CwjiE8uu3SqJfAU9sBb1ogDyHJAmbxj4r4HiKAMN5j`. Keep the decoded header with the response body. The seller does not keep a separate receipt store for buyers.

### 4. Outcomes after you send `PAYMENT-SIGNATURE`, and when retrying is safe

| Outcome | What you see | Was a payment submitted? | What to do |
|---|---|---|---|
| Success | `200`, data, `PAYMENT-RESPONSE` `success:true` | Yes, settled | Done. Do not retry. |
| Payment rejected before settlement (malformed, wrong amount, verify failure) | `402` **with a fresh `PAYMENT-REQUIRED`** | No | Safe to fix and pay again. |
| Handler error (bad mint → `400`, internal `5xx`) | `4xx/5xx`, no successful `PAYMENT-RESPONSE` | No: settlement is cancelled when the handler answers ≥ 400 | Fix the request; retrying is safe. |
| Settlement failed or uncertain (PayAI rejected, errored or timed out during `/settle`) | `402` with body `{}`, `PAYMENT-RESPONSE` `success:false` and an `errorReason`, **no `PAYMENT-REQUIRED`** | Possibly | Reconcile first (below). |
| Function timeout, dropped connection, `5xx` from the platform | No usable response | Possibly | Reconcile first (below). |

The server never answers an uncertain settlement with a fresh `PAYMENT-REQUIRED`. Only a pre-settlement rejection does that. Note that an uncertain settlement uses the same status code (`402`) as a pre-settlement rejection, so tell them apart by the header: `PAYMENT-REQUIRED` present means not paid; `PAYMENT-RESPONSE` with `success:false` means reconcile.

**Reconcile without paying twice (Solana):**
1. If `PAYMENT-RESPONSE` contained a `transaction`, query it (`getSignatureStatuses` / `getTransaction`). Finalized with `err: null` means you paid; do not pay again.
2. If not, list recent signatures on your USDC token account (`getSignaturesForAddress`) and look for a `TransferChecked` of the exact amount into `D4CwjiE8uu3SqJfAU9sBb1ogDyHJAmbxj4r4HiKAMN5j` after the time of your request.
3. A transfer that is briefly absent is not proof that it will not land. Check `isBlockhashValid` for the blockhash you signed. Only once it returns `false` (the blockhash has expired, roughly 60–90 s after signing) can that unlanded transaction never land, and a new payment is safe.
4. If you paid but got no data, contact support (below) with the signature. The paid request itself is not replayable: a new GET needs a new payment.

### 5. Support
https://x.com/ProfitzDigital. Please include the transaction signature and UTC time.

## Settlement evidence (Solana mainnet)

End-to-end captures from **operator test payments** made on 2026-10-18 from the operator's test wallet `GB9E9Vk5cTwbUa5xbpvNGtHKUsii18qiub8ST41tna9W` (funded by the payTo in tx [5TCm1UN2…GYE4](https://solscan.io/tx/5TCm1UN2eASKW1kdNvbE8UFeb57JRCHg7f2jKCJrPzi1Zhu2efWEeAJs8BEeNWDsGb7L9hcQ1Fpk7UkZg4vHGYE4), 0.02 USDC). These are not customer activity. The client was `@x402/fetch` + `@x402/svm` `ExactSvmScheme`. Each transaction was checked via public RPC `getTransaction` at `finalized` commitment: `err: null`, fee payer `CjNFTjvBhbJJd2B5ePPMHRLx1ELZpa8dwQgGL727eKww` (PayAI), and a `TransferChecked` from `GYQJaLaVHxWoRH1tDgSjXnziMdX5hzT8TnN5G7nEoo6P` (test wallet USDC account) to `D4CwjiE8uu3SqJfAU9sBb1ogDyHJAmbxj4r4HiKAMN5j` (payTo USDC account).

### A. Risk endpoint: operator test

| Field | Value |
|---|---|
| Request | `GET https://trench-lessons.vercel.app/api/signals/risk/DFMt2FyLpB6ekPNAzVErLXgpSnJ9CRf1VnxBAkTLpump`, 2026-10-18 15:23:45 UTC |
| Amount | 10000 atomic units (0.01 USDC) |
| Response | `200`: `{"mint":"DFMt2FyLpB6ekPNAzVErLXgpSnJ9CRf1VnxBAkTLpump","mocked":false,"network":"solana-mainnet (read-only RPC)","flags":{"curveSkipPool":{"value":false,"status":"ok","confidence":"high","detail":{...}},"unlockedLp":{"value":false,"status":"ok","confidence":"high",...},"mayhemMode":{"value":false,"status":"ok","confidence":"high",...},"bundleHandoff":{"value":false,"status":"ok","confidence":"low",...}},"riskScore":0,"scoredFlags":4,"elapsedMs":226,"asOf":"2026-10-18T15:23:47.380Z","disclaimer":"Heuristic, read-only on-chain checks. ..."}` |
| Settled by | PayAI, slot 458483425, block time 2026-10-18 15:23:47 UTC |
| Transaction | https://solscan.io/tx/fkBM1NpeSXapntXDrJGWB657RZvM9v9ocykk2XTk9VDeJvGvpn5PprmLKUbrmc82SL2NoeCoPBCMAhSeu7hNrhD |

Decoded `PAYMENT-RESPONSE`:
```json
{"success": true, "payer": "GB9E9Vk5cTwbUa5xbpvNGtHKUsii18qiub8ST41tna9W", "transaction": "fkBM1NpeSXapntXDrJGWB657RZvM9v9ocykk2XTk9VDeJvGvpn5PprmLKUbrmc82SL2NoeCoPBCMAhSeu7hNrhD", "network": "solana:5eykt4UsFv8P8NJdTREpY1vzqKqZKvdp"}
```

### B. Feed endpoint: operator test

| Field | Value |
|---|---|
| Request | `GET https://trench-lessons.vercel.app/api/lessons/feed?days=1`, 2026-10-18 15:23:50 UTC |
| Amount | 5000 atomic units (0.005 USDC) |
| Response | `200`: `{"generatedAt":"2026-10-18T15:23:52.360Z","count":1,"feed":[{"date":"2026-10-17","findings":[{"topic":"Bitquery, FOMO app (Oct 17): ...","evidence":"A dataset","points":[...]},{"topic":"pump.fun: new 0.45% platform fee on app and web trades from Oct 17",...},...],"sources":[...]}],"disclaimer":"Educational research only. ..."}` |
| Settled by | PayAI, slot 458483446, block time 2026-10-18 15:23:52 UTC |
| Transaction | https://solscan.io/tx/5dWbfEww4PosucPZrHh81FiEDU6uGxgU6NqWtEaWT1z49h1XjkUAv4RdbQQWnxbmtwKKmh3K7vgqtNMEfyGSUXCo |

Decoded `PAYMENT-RESPONSE`:
```json
{"success": true, "payer": "GB9E9Vk5cTwbUa5xbpvNGtHKUsii18qiub8ST41tna9W", "transaction": "5dWbfEww4PosucPZrHh81FiEDU6uGxgU6NqWtEaWT1z49h1XjkUAv4RdbQQWnxbmtwKKmh3K7vgqtNMEfyGSUXCo", "network": "solana:5eykt4UsFv8P8NJdTREpY1vzqKqZKvdp"}
```

Bodies are abbreviated with `...`; they contain only public research and on-chain data. The payer is the operator's own test wallet, so it is not redacted.

## Earlier operator test payments (amount-only evidence)

These four earlier payments came from the same test wallet, which the payTo funded at 2026-10-16 00:01:17 UTC. On-chain they match the newer captures: finalized, `err: null`, PayAI fee payer, `TransferChecked` into `D4CwjiE8uu3SqJfAU9sBb1ogDyHJAmbxj4r4HiKAMN5j`. Their response bodies and `PAYMENT-RESPONSE` headers were not retained, so they are evidence of amount and recipient only. The endpoint is inferred from the price.

| # | Block time (UTC) | Slot | Amount | Inferred endpoint | Transaction |
|---|---|---|---|---|---|
| 1 | 2026-10-16 00:01:36 | 457429969 | 10000 (0.01 USDC) | risk | https://solscan.io/tx/5aiNR3XnUtd4JPVKA2n1CPj2UYBQFwBU4SdrDwcbcUu623K6KqDCVRNcAG8n3Bug4ZFA43h4dtbCa2T5w2AFaWcZ |
| 2 | 2026-10-16 00:06:31 | 457431320 | 5000 (0.005 USDC) | feed | https://solscan.io/tx/5efqUhFgxa2KuvAxuvyg2zpQBfeTp8orSzPHvHsCKpqJ2dtAeZkBc7ro3rs95ajChYMiQwMV9QViN2WTU2JUJxW2 |
| 3 | 2026-10-16 00:06:39 | 457431356 | 10000 (0.01 USDC) | risk | https://solscan.io/tx/2HusZoogZCpGN3FdPBndHvqT5czqsmNoxCzwibD1pk5yAKprEtvVaBYVKxDFLt8d2C9rRzVgcJQx1KBzQ5DKNHV2 |
| 4 | 2026-10-16 00:43:37 | 457441636 | 5000 (0.005 USDC) | feed | https://solscan.io/tx/4o7wowURd1wKfurV7ukoV3hbmEpTkvGT4s3VgWaYRL8DbXkfGNHYTheCNxeX2SpqmeAusYfpKuFnj6nCKyCZ8Cj2 |

No keys, credentials or usable payment authorizations are included.
