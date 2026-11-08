# Pharos Atlas

## Basic details

- Project name: Pharos Atlas
- Publisher/operator: Pharos Atlas / Summerall Capital; founder Clayton Summerall.
- What does it do? Pharos Atlas connects 200 specialist sources with stored representations in 10 languages and U.S. state, city, neighborhood and landmark navigation. Localized HTML and structured APIs are resource-specific. The 197 fixed English snapshots are separate purchases; coverage varies by source and route.
- Type: APIs & data
- Official website: https://pharosatlas.com
- Logo URL: https://pharosatlas.com/brand/pharos-mark.png
- Documentation/getting started: https://pharosatlas.info/network ; exact offset-printing request and payment instructions: https://billing.pharosatlas.com/payments?product=offset-printing-review
- Public support/contract destination: https://summerall.capital/ — the official https://pharosatlas.com/commercial page links this as “Support and existing contracts.” This proposal does not add a new response-time or support-service promise.
- Public repository: The production API source is not published; no public source repository is claimed.

## Network representations and resource selection

- Buyer network and source navigation: https://pharosatlas.info/network . Public source registry: https://pharosatlas.info/.well-known/pharos-network.json .
- The 200 specialist sources have existing stored core representations in ten locale IDs: `en` English, `es` Spanish, `zh` Simplified Chinese, `fr` French, `de` German, `pt` Brazilian Portuguese, `ar` Arabic, `hi` Hindi, `ja` Japanese and `ko` Korean. The HTML presentation tags for `zh` and `pt` are `zh-Hans` and `pt-BR`; API selectors remain `zh` and `pt`. Arabic is right-to-left.
- Locales select stored representations, not translation on request. Non-English material has declared machine/model-assisted, unreviewed provenance; no professional language review is claimed. A representation locale does not establish the language of underlying primary-source documents.
- Source HTML selects the existing locale in `/{locale}/...`. Structured JSON uses `language` only where the source operation documents it; it is not a global selector. Inspect that source's OpenAPI before choosing an existing route, method, query and response type. Manifests and taxonomies may contain multilingual fields without accepting a language query.
- Existing U.S. navigation uses 50 canonical state slugs, then source-issued city, neighborhood and landmark records and links. Use returned child slugs and paginated collection links; raw geographic names, IDs, coordinates and provenance remain source values. Coverage is uneven and does not establish every U.S. place or every locale/geography combination. No country, county, ZIP, address or radius selector is offered.
- Guide and answer collections exist for 68 sources; the other 132 sources lack those collections and are not offered as guide/answer purchases. Missing, empty or unavailable source combinations are excluded. Each purchase covers one exact existing resource and representation under its own input/output contract and canonical quote.
- The 197 named fixed English JSON snapshots are a separate catalog. Network locale or location selection does not translate, alter or multiply those immutable products. Ten supported locale IDs are not a claim of ten times measured distinct content or paid-delivery verification.
- The offset-printing resource below is one bounded example with existing PayAPI evidence. Its parameter-free GET, English bytes, price and payment identity remain unchanged; the attestation does not cover the network's other resources.

## Networks and ownership

- Supported payment network in this proposal: Base mainnet, CAIP-2 `eip155:8453`.
- Official project reference: https://pharosatlas.com/commercial links the buyer catalog, Pharos Atlas network and Summerall Capital for support/existing contracts. https://pharosatlas.info/network describes the source collection.
- This proposal is submitted on behalf of the project owner through the existing `summerallclayton-ops` account. No wallet ownership signature is supplied or claimed.
- Merchant receiving address on Base: `0x6Ac716842c089AaeeC8B3041F8096e0823254A84`.
- Public existing marketplace reference: https://payapi.market/api/pharos-atlas-offset-printing-review-reference
- No transaction-count, unique-customer, organic-demand or revenue-growth claim is made. Wallet totals can include controlled tests and unrelated resource activity.

## Payments — one evidenced API resource

- Exact endpoint: `GET https://billing.pharosatlas.com/api/x402/resources/offset-printing-review`
- Input: No request body or topic parameters. This retrieves a fixed snapshot; it does not accept arbitrary printing questions, uploaded job files or samples.
- Facilitator used: Coinbase Developer Platform x402, https://api.cdp.coinbase.com/platform/v2/x402 . Pharos Atlas is a merchant, not a new facilitator applicant.
- Payment protocol: x402 v2, `exact`; EIP-3009 authorization flow.
- Price: `0.01` native USDC per immutable English reference snapshot; `10000` atomic units.
- Token contract on Base: `0x833589fCD6eDb6E08f4c7C32D4f71b54bdA02913`; decimals: `6`.
- Public successful Base payment: https://basescan.org/tx/0x9765f1c8268fb5bb8afbe3be146f8fb637d1228ee0f1a725add11fbd95f73b90
- Evidence scope: The existing PayAPI listing states that PayAPI paid from its own wallet and received real data. The published transaction matches the reconciled native-USDC receipt. PayAPI publishes no client payload checksum. This is one-route provider-funded verification, not proof of full-network delivery or organic demand.

## Output contract and limits

- Format: `application/json`, `pharos.trade-review.v1`, English.
- Snapshot: `pharos-offset-printing-20261019-r1`; source date `2026-10-19`.
- Complete immutable reference: 4,050 UTF-8 bytes; SHA-256 `b5821acbf4e9bb6180bf6e6f469b221e635f18c2ed7a9f2d3fc67fbac9933d66`; response limit 24,576 bytes.
- Top-level fields: `schema`, `product`, `question`, `language`, `snapshot`, `source_date`, `site`, `review`, `subjects`, `provenance`. Review includes question/workflow arrays; subjects map named printing topics to editorial notes; provenance records source context and rights.
- Machine-readable complete nested schema and captured excerpt: https://billing.pharosatlas.com/openapi.json (operation `/api/x402/resources/offset-printing-review`, GET).
- Free catalog: https://billing.pharosatlas.com/.well-known/pharos-paid-products.json
- Captured excerpt, not the complete purchased response: `{"schema":"pharos.trade-review.v1","product":"offset-printing-review","language":"en","snapshot":"pharos-offset-printing-20261019-r1","review":{"questions":["Which artwork and plate revision define the job?"],"workflow":["Identify the job specification and materials"]}}`
- Limitations: Fixed editorial reference only. No inspection of a job, machine, material or sample; no certification, professional approval, compliance determination or work authorization. Source dates do not establish current conditions or continuous updates.
- Rights: `search=yes`, `ai-input=yes`, `ai-train=no`. Single purchased snapshot for internal reference. Bulk redistribution, sublicensing and a training license are not conferred.

## Catalog scope

This application represents one Pharos Atlas network/provider: 200 specialist sources with resource-specific stored locale and U.S. location navigation, alongside the separate catalog of 197 fixed English snapshots. Availability, source provenance, MIME type and selectors are determined by each exact existing resource. The offset-printing reference is the evidenced example; PayAPI's verification is limited to that route. No complete geography/locale Cartesian product, full-network paid delivery or fabricated MCP service is claimed. Unavailable content is excluded.

## Website application

- Canonical application path: https://x402blockchains.com/ai-agents-apps/?view=submit
- Existing application: No earlier Pharos proposal or matching directory search result was observed on October 26, 2026.
- This is a free listing review request; no sponsored promotion or paid plan is requested.
- Review status: Submitted proposal is not automatic approval, publication or transaction indexing. No credentials, private contact information, signed payment authorizations or private result bodies are included.

