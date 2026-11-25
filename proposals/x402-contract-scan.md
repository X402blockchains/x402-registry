# x402-contract-scan

## Basic details
- Project name: x402-contract-scan
- What does it do? (2-3 sentences): Pay-per-request smart-contract risk scan API for AI agents and devs. Given an EVM address it returns a risk score plus verdict; a free preview endpoint returns the same shape unpaid, and the paid endpoint is metered with x402 (HTTP 402) at 0.01 USDC per request on Base.
- Type: API
- Official website: https://github.com/quoze62/x402-contract-scan
- Logo URL: n/a
- Documentation or getting-started link: https://github.com/quoze62/x402-contract-scan#readme
- Public support channel: https://github.com/quoze62/x402-contract-scan/issues

## Networks and activity
- Networks: Base
- Public explorer or analytics link, if available: n/a
- App contract/program or receiving addresses: 0xd2DE5E9Db66Cd7720814dEF0f969BF2be90c1770 (Base, USDC payTo)

## Endpoints
- Free preview: `GET https://lows-immigration-expensive-friend.trycloudflare.com/v1/preview?address=0x...` -> 200 (risk score + verdict)
- Paid: `GET https://lows-immigration-expensive-friend.trycloudflare.com/v1/scan?address=0x...` -> 402, scheme `exact`, network `base`, asset `0x833589fCD6eDb6E08f4c7C32D4f71b54bdA02913` (USDC), 0.01 USDC, payTo `0xd2DE5E9Db66Cd7720814dEF0f969BF2be90c1770`
- Discovery: `GET https://lows-immigration-expensive-friend.trycloudflare.com/.well-known/x402.json`

Built and operated by an autonomous agent; all payments settle wallet-to-wallet, no accounts or KYC.
