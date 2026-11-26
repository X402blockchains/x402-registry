# Quantum Shield

## Basic details
- Project name: Quantum Shield
- Description: Quantum Shield provides website-risk checks, wallet and token evidence, and resource APIs for people and software agents. Reports distinguish available evidence from unavailable coverage and do not guarantee asset or website safety. We are applying for an app/API directory listing; this is not an application to operate a payment facilitator.
- Type: App / resource API / agent tooling
- Official website: https://quantumsshield.com/
- Resource catalogue: https://quantumsshield.com/resources
- Payments page: https://quantumsshield.com/payments
- Logo URL: https://raw.githubusercontent.com/QuantumShieldOfficial/quantum-shield/main/logo.png
- Current paid-resource OpenAPI: https://quantumsshield.com/api/resources/openapi.json
- Documentation: https://quantumsshield.com/docs
- Public repository: https://github.com/QuantumShieldOfficial/quantum-shield
- Official X: https://x.com/quantumsshield
- Public support/community: https://t.me/QuntumsShield
- Announcement channel: https://t.me/QuntumShield

## Product scope
The public catalogue advertises free Website Risk Check and Wallet Overview tools, alongside per-request paid reports. Paid reports include token metadata, explicit token allowance checks, multichain native-account summaries, recent transfer history, destination-label lookups, wallet comparison, contract privilege signals, account-state readiness reports, evidence reports and caller-supplied snapshot comparisons.

Website deep inspection is a bounded public-code review, not full browser execution or a security audit. Multichain account snapshots are not bridge tracing. Transaction simulation and QR decoding are explicitly in development and are not submitted as live capabilities. A Quantum Readiness report is a checklist and evidence report, not quantum-resistant wallet protection.

## Networks and activity
- Payment settlement network advertised by the current payment page: Base mainnet, chain ID 8453 (eip155:8453).
- Data-analysis networks: Ethereum, Base, BNB Chain, Arbitrum and Polygon. These analysis networks must not be presented as five supported payment networks.
- Public payment recipient displayed in the resource catalogue (Base): 0x26a829DaE4942A40857023021bada0969f02d2db
- Explorer reference: https://basescan.org/address/0x26a829DaE4942A40857023021bada0969f02d2db
- Direct transfers to the recipient do not buy API access.
- No independently established project transaction count, customer count or volume is claimed in this proposal. Activity metrics should remain unavailable until an attributable feed and coverage are reviewed.
- Representation: submitted by QuantumShieldOfficial, the account maintaining the public project repository linked from the official website.

## Payments
- Example paid endpoint: POST https://quantumsshield.com/api/resources/token-check
- Example input: {"chain":"base","address":"0x833589fCD6eDb6E08f4c7C32D4f71b54bdA02913"}
- Advertised price for this report: 0.02 USDC per request. Consult the live offer before authorizing payment.
- Payment version: the current paid-resource OpenAPI describes x402 v2 and HTTP 402 Payment Required. The exact supported scheme must be confirmed from a retained live payment challenge rather than inferred from the price.
- Advertised settlement asset: native USDC on Base; token contract 0x833589fCD6eDb6E08f4c7C32D4f71b54bdA02913, 6 decimals. No QUS payment contract is claimed.
- Facilitator identification: the current /payments status and paid-resource OpenAPI identify Coinbase CDP. The resource-catalogue footer instead mentions X-Pay. These public descriptions require alignment before a facilitator-specific relationship can be confirmed; this application does not claim a verified live XPay integration.
- Expected response semantics in the current schema: 200 evidence report, 202 settlement pending, 402 payment required, and explicit input/quota/provider errors. A pending payment should be recovered rather than authorized again.
- Successful payment transaction evidence: not supplied with this initial proposal. A successful Base settlement explorer link and the matching redacted application response are still required to verify the paid integration. No transfer is being represented as an x402 purchase without that evidence.
- Facilitator-only supported/verify/settle URLs and relayer addresses: not applicable; Quantum Shield is applying as a merchant app/API, not a facilitator.

## Documentation alignment and remaining evidence
The current /payments page and resource OpenAPI advertise enabled paid reports. The older /docs payment section and public GitHub API guide still describe x402 as planned. Those older descriptions need updating to match the deployed product. The public resource OpenAPI currently documents the token-check operation; complete schemas for other advertised paid operations should be supplied for their individual review.

Before approval of the paid integration, we will provide:
1. A retained x402 challenge identifying the scheme, chain, asset, recipient and price, without publishing a signed authorization.
2. A successful Base settlement transaction link matched to the purchased report/receipt.
3. Consistent facilitator identification and updated public payment documentation.
4. Coverage details for any activity feed; no inferred usage or revenue totals.

## Website application
- Application route: this GitHub proposal.
- Separate website application reference: none.
- Related previous proposal: none found for Quantum Shield.
- Requested status: submitted for review only. Please leave this proposal pending; no approval, merge, indexer activation or website publication is requested at this stage.

Quantum Shield
