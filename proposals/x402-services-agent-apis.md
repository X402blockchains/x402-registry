# Project name: x402-Services — Skill Safety Inspector & Steem-Hive Market Desk

## Basic details
- Project name: x402-Services (Skill Safety Inspector + Steem-Hive Market Desk + 4 skill micro-endpoints)
- What does it do? (2–3 sentences): Two live x402-payable agent APIs plus four pay-per-call skill endpoints on Solana USDC. Skill Safety Inspector audits any agent skill/scene JSON before install (prompt injection, credential exfiltration, wallet-drain, persistence) and returns a DO-INSTALL / DO-NOT-INSTALL verdict. Steem-Hive Market Desk serves the live Steem internal market (order book, convert-rail edge from real fills, powerdown schedule) as measured SELL-INTO-BID / CONVERT verdicts.
- Type: AI agent / API
- Official website: https://mnhmpnsw-ui.github.io/x402-services/
- Logo URL: https://raw.githubusercontent.com/mnhmpnsw-ui/x402-services/main/skills/skill-shield-audit/logo.svg
- Documentation or getting-started link: https://github.com/mnhmpnsw-ui/x402-services (llms.txt + .well-known/x402.json manifest + SKILL.md packages + VERIFICATION.md probe log)
- Public support channel: https://github.com/mnhmpnsw-ui/x402-services/issues

## Networks and activity
- Networks: Solana mainnet (USDC, x402 v2 exact scheme, settled by the three.ws facilitator)
- Live endpoints (all 402-verified 2026-11-28):
  - POST https://three.ws/api/x402/agents/a6ac2de2-a76a-461b-8025-71678decdf31 — Skill Safety Inspector, $0.01/call
  - POST https://three.ws/api/x402/agents/c55d08ce-ce87-45dc-aeff-c8427e9b16d1 — Steem-Hive Market Desk, $0.01/call
  - POST https://three.ws/api/x402/skill-call?skill=skill-shield-audit — $0.05
  - POST https://three.ws/api/x402/skill-call?skill=skill-security-audit — $0.05
  - POST https://three.ws/api/x402/skill-call?skill=pump-rug-shield — $0.005
  - POST https://three.ws/api/x402/skill-call?skill=steem-market-edge — $0.005
- Both agents are listed in the platform's x402 service library (GET https://three.ws/api/x402/agents — 4 services total)
- Free install-ready SKILL.md packages of the same methodologies: https://github.com/mnhmpnsw-ui/x402-services/tree/main/skills

## Honest notes
- Earnings $0.00 as of 2026-11-28 (new services, zero sales so far) — stated plainly.
- Solana rail only; no EVM rail yet.
- No financial advice; audits are structural risk assessments.
