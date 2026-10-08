<p align="center"><img src="https://raw.githubusercontent.com/X402blockchains/x402blockchain/main/branding/github-header.svg" alt="X402blockchains" width="100%"></p>

# x402 Registry

The community proposal desk for [X402blockchains](https://x402blockchains.com). Submit APIs, AI agents and facilitators through a GitHub issue or pull request.

**Status:** manual review. This repository does not automatically publish listings or start indexing wallets.

## Apply as a facilitator

**[Apply as a facilitator →](https://github.com/X402blockchains/x402-registry/issues/new?template=facilitator.yml)**

No coding is required: sign in to GitHub, complete the form and submit your application.

| Prepare | Details |
|---|---|
| Identity | Name, official website, logo, documentation and public support link |
| Capabilities | Base, Solana or BNB Chain; mainnet identifiers; x402 versions and schemes |
| Endpoints | Public facilitator URL and supported, verify and settle endpoint URLs |
| Addresses | Signer/relayer and router addresses, clearly separated from seller wallets |
| Evidence | Successful settlement hashes for each chain and public ownership proof |
| History | First settlement date in UTC, deployment block/slot, tokens and decimals |

**Review process:** application → maintainer checks → requested corrections → approved integration → indexing and publication. These are manual steps; submitting or merging a proposal does not automatically deploy the website. XRP applications may be discussed as planned support.

Prefer a pull request? Fork this repository, add a Markdown proposal under `proposals/your-facilitator.md` using the fields above, then open a PR and link any existing application. Use an official logo URL or include a logo you have permission to submit. Never include API keys, private keys or signed payment authorizations.

## Request a listing

1. Fork this repository.
2. Copy the template below into `proposals/your-project.md`.
3. Replace every placeholder with public information. Include a working logo.
4. Open a pull request describing ownership and payment evidence.
5. A maintainer reviews the endpoint, logo, network and addresses before registering approved metadata in the explorer.

Alternatively open an issue using the same fields. Do not post private contact details, credentials or signed payment authorizations.

## Proposal template

```markdown
# Project name
- Type: API / AI agent / facilitator / both
- Description:
- Website (HTTPS):
- Logo (HTTPS):
- Documentation:
- Public repository:
- Networks and chain identifiers:
- Paid resource URLs and HTTP methods:
- x402 version and payment scheme:
- Token contract or mint, decimals:
- Seller payment recipient addresses:
- Facilitator URL and supported endpoint:
- Facilitator signer / relayer addresses (if applicable):
- Example successful settlement hashes and explorer links:
- Ownership evidence (domain-hosted proof or public project reference):
- Public support channel:
```

## Review criteria

A logo must load and represent the project. Addresses must belong to the claimed network. A seller receiving payments is not automatically the facilitator submitting settlements. Projects serving both roles must provide evidence for each role.

Base, Solana and BNB Chain are the initial review scope; XRP is planned. Network inclusion does not guarantee historical coverage. New facilitator support may need a tested indexing adapter.

## Updates and corrections

Use a new issue or pull request referencing the existing listing. Include affected addresses, transaction hashes and UTC dates. Never submit invented counts or volumes. Approval is not a security audit; no review deadline or listing guarantee is implied.

[Explorer source and contribution guide](https://github.com/X402blockchains/x402blockchain) · [Follow updates](https://x.com/x402blockchains)
