# Solana Paid Leaderboard (Dream Sheep Jump)

A leaderboard architecture where local play is free and global publication is paid + on-chain.

## 2-minute project summary
### What the MVP does now
- Player plays locally and saves local scores for free.
- Player can submit score to global board by signing a Solana Devnet transaction.
- Program enforces fee + score update in one flow.
- Program stores **best score per player** (not every run).
- Frontend/API reads on-chain accounts and renders global top scores.

### What MVP intentionally does not do
- Full anti-cheat or tamper-proof gameplay verification.
- Per-action on-chain logging.
- zk/zkVM score validity proofs.
- Binary attestation verification.

## Why this MVP shape
- **Hackathon-feasible** under tight timeline.
- **On-chain source of truth** for global leaderboard is enough for demo integrity.
- **Best-score-per-player** keeps storage/rent/indexing manageable.
- Leaves clean extension points for session verification later.

## Why Solana + Anchor
- Solana gives fast/cheap transaction rails suitable for micro-fee leaderboard submits.
- Anchor accelerates program development with typed accounts, account constraints, and IDL-driven client integration.

## Documentation map
- `docs/PROJECT_OVERVIEW.md`
- `docs/PRD.md`
- `docs/SRD.md`
- `docs/ARCHITECTURE.md`
- `docs/ANTI_CHEAT_ROADMAP.md`
- `docs/MVP_VS_ROADMAP.md`
- `docs/GLOSSARY.md`
- `docs/TRUST_MODEL.md`
- `docs/ARCHITECTURAL_DECISIONS.md`
- `docs/IMPLEMENTATION_NOTES.md`
- `docs/diagrams/` (context, use-case, dataflow, class, sequence, lifecycle)

## Design guardrails
- Don’t overclaim anti-cheat in MVP.
- Keep current-state and roadmap-state explicitly separated.
- Keep global board derivable from chain data.
