# Solana Paid Leaderboard (Dream Sheep Jump)

A mobile-friendly Solana game architecture where:
- **Local leaderboard is free** (local storage), and
- **Global leaderboard is paid + on-chain** (Devnet for MVP).

The chain is the global source of truth for published scores.

---

## Project Status

### MVP (current direction)
- Dream Sheep Jump gameplay remains client-side.
- Local score save is free and immediate.
- Global score submission requires a micro-payment and on-chain write.
- Best-score-per-player pattern is used on-chain.
- Frontend/API reconstructs global ranking from on-chain data.

### Not in MVP
- Full anti-cheat.
- Zero-knowledge score correctness proofs.
- Per-action on-chain logging.
- Remote attestation of game binary integrity.

### Future direction (research/roadmap)
- Session/channel model with cryptographic linking.
- Optional tamper attestation.
- Hash-linked action transcript (or commitment tree).
- Verified-run badges and optional zk/zkVM validation paths.

---

## Why this architecture
1. **Hackathon-feasible**: scope fits a Monday submission timeline.
2. **Strong demo narrative**: pay-to-publish + verifiable on-chain leaderboard.
3. **Upgradeable**: anti-cheat can evolve without breaking MVP contract surface.

---

## What is Anchor?
Anchor is a Rust framework for Solana programs (smart contracts). It provides:
- account validation via `#[derive(Accounts)]`
- IDL generation for clients
- cleaner instruction handlers and typed account models
- faster test/deploy workflow

Anchor is the recommended stack for this project’s on-chain score program.

---

## Documentation Map
- `docs/PROJECT_OVERVIEW.md` — high-level concept and boundaries
- `docs/PRD.md` — product requirements
- `docs/SRD.md` — software requirements and interfaces
- `docs/ARCHITECTURE.md` — end-to-end system design + rationale
- `docs/ANTI_CHEAT_ROADMAP.md` — session/channel cryptographic roadmap
- `docs/diagrams/use-case.md` — use-case diagram (MVP + future lane)
- `docs/diagrams/dataflow.md` — dataflow (MVP and future anti-cheat path)
- `docs/diagrams/class-diagram.md` — initial class model
- `docs/REFERENCES.md` — references and inspiration

---

## Principles
- Keep MVP simple and demonstrable.
- Keep on-chain truth minimal and explicit.
- Keep future cryptographic claims clearly labeled as roadmap.
