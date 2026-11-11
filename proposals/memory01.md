# Memory01

## Basic details
- Project name: Memory01
- What does it do? (2–3 sentences): Agentic memory service for AI agents. Free to store memories (key-value with metadata), paid to search with keyword matching. First 3 searches/day free per agent, then $0.01 USDC. Write token authentication ensures memory isolation — no one can read your memories without your token. Subscription plans available: Starter ($2/500 credits), Pro ($9/mo unlimited), Enterprise ($20/mo unlimited+priority).
- Type: API
- Official website: https://memory.node01.org/
- Logo URL: https://memory.node01.org/favicon.ico
- Documentation or getting-started link: https://memory.node01.org/llms.txt (OpenAPI: https://memory.node01.org/openapi.json)
- Public support channel: enrico@node01.org

## Networks and activity
- Networks: Base
- Public explorer or analytics link, if available: https://www.x402scan.com/server/eb0ca4e3-4f4b-4912-ab75-a8f26fa61416 (origin registered); operator test settlements exist
- App contract/program or receiving addresses, with their networks, if available: Base (eip155:8453) payee 0xe9a827d9453e9b18040c25bb492a568ddd827549
- Proof that you represent the project: domain ownership (memory.node01.org resolves to our server)

## Payments — only if your product accepts payments
- Paid endpoint and HTTP method: POST /api/memory/search ($0.01 USDC per search after free tier), POST /api/memory/subscribe ($2/$9/$20 USDC)
- Price model: freemium — 3 free searches/day, then $0.01/search. Subscription plans: Starter ($2/500 credits), Pro ($9/mo unlimited), Enterprise ($20/mo unlimited+priority)
- Payment rail(s): x402 (USDC on Base, eip155:8453)
- Settlement address(es): 0xe9a827d9453e9b18040c25bb492a568ddd827549 (Base)
- Refund / dispute policy: No refunds for completed searches. Subscription credits never expire.

## Ownership reference
- Contact email: enrico@node01.org
- Domain: memory.node01.org (DNS resolves to our server)