# Nettrux

## Basic details
- Project name: Nettrux
- What does it do? (2–3 sentences): Nettrux is a California freight broker and the first 3PL on x402. We are building agent-to-agent shipping so a shipper's AI agent can quote a freight lane on our API and propose a booking through the x402 handshake, while a named human still approves every mint. The portal already runs live multi-carrier LTL, FTL and air for human shippers.
- Type: API
- Official website: https://www.nettrux.ai
- Logo URL: https://www.nettrux.ai/opengraph-image
- Documentation or getting-started link: https://www.nettrux.ai/agents
- Public support channel: dispatch@nettrux.net / https://x.com/nettrux

## Networks and activity
- Networks: Base (testing settlement only; public production settlement flagged off)
- Public explorer or analytics link, if available: Not applicable for a public paid resource yet
- App contract/program or receiving addresses: Not published for a public pay-and-book surface
- Proof that you represent the project: https://www.nettrux.ai , https://x.com/nettrux , https://dev.to/nettrux

## Payments — only if your product accepts payments
Not applicable for a public unpaid pay-and-book listing today.
- Paid endpoint and HTTP method: Not applicable — public pay-and-book / real-money settlement gates are flagged off (`X402_REAL_MONEY_SETTLEMENT_LIVE: false`, `EDGE_X402_DISCOVERY_PUBLISHED: false`). Discovery pointer: https://www.nettrux.ai/.well-known/x402 (resources array empty). Authenticated commit handshake is documented on Edge OpenAPI for bearer agents, not as a public open endpoint.
- Facilitator used: Not applicable for public listing
- Payment scheme/version: x402 v1 documented on authenticated commit; not claiming a public challenge
- Token contract/mint and decimals: Not applicable for public listing
- Successful payment transaction link: Nettrux has settled a real x402 USDC payment on Base in testing (internal). Not submitting a public explorer link in this proposal until counsel/ops approve sharing it.
- Facilitator applicants: Not applicable

## Website application
- Website application reference, if you have one:
- Related issue or previous pull request, if any:
