# Change Summary

This patch repurposes the repo from a Solana paid leaderboard game into a **Solana delegated checkout agent** for time-sensitive purchases.

## Updated files
- `README.md`
- `docs/PROJECT_OVERVIEW.md`
- `docs/PRD.md`
- `docs/SRD.md`
- `docs/ARCHITECTURE.md`
- `docs/ANTI_CHEAT_ROADMAP.md` *(content repurposed as future delegated-checkout roadmap)*
- `docs/MVP_VS_ROADMAP.md`
- `docs/diagrams/system-context.md`
- `docs/diagrams/dataflow.md`
- `docs/diagrams/use-case.md`

## Main concept shift
Old concept:
- paid on-chain game leaderboard

New concept:
- user-authorized delegated checkout/payment agent for time-sensitive drops, tickets, or limited registrations

## Key architectural changes
- `PlayerScore`-style state replaced with `PurchasePolicy` and `PurchaseReceipt`
- score submission flow replaced with policy creation + bounded execution flow
- anti-cheat/session roadmap replaced with merchant reconciliation / attestation roadmap
- leaderboard UI replaced with policy / receipt status dashboard

## Important note
The file `docs/ANTI_CHEAT_ROADMAP.md` was kept for compatibility with the current doc map, but its content was rewritten to describe future delegated-checkout roadmap ideas. In the actual repo, consider renaming it later to something like `docs/DELEGATED_CHECKOUT_ROADMAP.md`.
