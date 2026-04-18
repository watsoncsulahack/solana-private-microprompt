# Solana Delegated Checkout Agent

A Solana-backed payment and authorization layer for **time-sensitive purchases** such as limited drops, ticket releases, and first-come-first-served registrations.

## 2-minute project summary
### What the MVP does now
- User creates a **purchase policy** with strict limits.
- User funds or pre-approves a capped spend for that policy.
- A delegated checkout agent can execute a purchase **only within those user-defined rules**.
- Solana Devnet records the policy, payment/authorization flow, and a purchase receipt.
- Frontend renders policy status, execution status, and auditable receipts.

### What MVP intentionally does not do
- Defeat anti-bot systems or bypass merchant protections.
- Guarantee access to scarce inventory.
- Provide unrestricted wallet delegation.
- Integrate with every merchant or payment processor.
- Launch on mainnet.

## Why this MVP shape
- **Hackathon-feasible** under tight timeline.
- Solves a real checkout pain point without overclaiming “drop sniping.”
- Demonstrates how Solana can act as a **constrained authorization + payment rail**.
- Keeps wallet risk bounded through explicit price, quantity, merchant, and expiry limits.
- Leaves clean extension points for merchant adapters, attestations, and richer automation later.

## Why Solana + Anchor
- Solana gives fast, low-cost transactions suitable for time-sensitive checkout authorization and receipts.
- Anchor accelerates program development with typed accounts, account constraints, and IDL-driven client integration.
- PDAs are a natural fit for user-scoped policies and purchase receipts.

## Documentation map
- `docs/PROJECT_OVERVIEW.md`
- `docs/PRD.md`
- `docs/SRD.md`
- `docs/ARCHITECTURE.md`
- `docs/ANTI_CHEAT_ROADMAP.md` *(repurposed as future delegated-checkout roadmap until renamed)*
- `docs/MVP_VS_ROADMAP.md`
- `docs/diagrams/` (context, use-case, dataflow)

## Design guardrails
- Don’t frame the product as an unfair “bot sniper.”
- Keep the current-state MVP and the future merchant-integrated roadmap explicitly separated.
- Keep all agent authority **bounded, user-consented, and auditable**.
