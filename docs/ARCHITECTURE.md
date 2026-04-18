# Architecture

## 1) System context
- **Player** interacts with game client.
- **Wallet** signs score submission transaction.
- **Anchor program** enforces fee + state update rules.
- **On-chain PDAs** persist global leaderboard source-of-truth.
- **Leaderboard UI/API** reads chain state and renders rankings.

(See `docs/diagrams/system-context.md`.)

## 2) Architectural rationale

### Why Solana for global leaderboard
- Fast confirmation and low fees fit micro-fee score submissions.
- Public verifiability of published global state.
- Easy explorer-based demo proof for judges.

### Why Anchor
- Faster development with typed account constraints.
- Cleaner account validation and instruction handling.
- IDL-driven client integration.

### Why PDAs
- Deterministic account addresses for per-player score state.
- No private key required for program-owned account derivation.
- Natural fit for `(game_id, player)` best-score records.

### Why best-score-only on-chain
- Lower cost and lower complexity.
- Enough to prove a ranked global board.
- Avoids bloating chain with per-action/per-run data in MVP.

## 3) Current trust boundary
- **Trusted for MVP:** payment/publication integrity and deterministic ranking from on-chain accounts.
- **Not yet trust-minimized:** game runtime integrity and client score authenticity.

## 4) Current-state flow
1. Player plays locally.
2. Local score saved freely.
3. Player connects wallet and submits global score.
4. Program validates fee/config and updates PlayerScore PDA.
5. Leaderboard read path queries chain and renders top-N.

(See sequence diagrams in `docs/diagrams/`.)

## 5) Why anti-cheat is deferred
- Full anti-cheat is a separate research-heavy subsystem.
- Hackathon objective is clear on-chain publication integrity first.
- We intentionally preserve extensibility points for stronger verification later.

## 6) Future verification architecture (non-MVP)
- Session/channel id created at run start.
- Optional pre-session integrity assertions.
- Hash-linked action records with monotonic counters.
- Transcript commitment root attached to submission.
- Optional replay/proof verifier and verified-run badge classes.

Detailed roadmap: `docs/ANTI_CHEAT_ROADMAP.md`.

## 7) Open implementation gaps (code)
- Program implementation of Config PDA + PlayerScore PDA.
- Instruction handlers and account constraints in Anchor.
- Wallet/submit UX and tx confirmation states.
- Chain indexer/read adapter and deterministic sort tests.
