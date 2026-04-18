# Solana Paid Leaderboard (Dream Sheep Jump)

Pay-to-submit global scores on Solana devnet, with local free leaderboard + on-chain global replayability.

## Concept
- **Local leaderboard**: free, stored locally on device/browser.
- **Global leaderboard**: score submission requires a micro payment, then score is recorded on-chain.
- **Reconstructability**: global top scores can be rebuilt from chain data only.
- **Anti-cheat direction (v2)**: session commitments + optional ZK proof flow inspired by projects like ZK Battleships.

## Why this direction
- Feasible for mobile-hosted hackathon demo by Monday.
- Reuses existing local tooling and web stack.
- Strong monetization and verification narrative.

## What is Anchor?
Anchor is a Rust framework for Solana programs (smart contracts). It provides:
- account validation via `#[derive(Accounts)]`
- IDL generation for clients
- cleaner instruction handlers
- easier testing/deployment for Solana apps

In this project, Anchor is the recommended way to build the on-chain score program.

## MVP Scope
- Devnet only.
- Dream Sheep Jump as reference game.
- On-chain score submission for global board.
- Payment gate enforced by program instruction.
- Local leaderboard in browser storage.

## Docs
- `docs/PROJECT_OVERVIEW.md`
- `docs/PRD.md`
- `docs/SRD.md`
- `docs/diagrams/use-case.md`
- `docs/diagrams/dataflow.md`
- `docs/diagrams/class-diagram.md`
- `docs/REFERENCES.md`
