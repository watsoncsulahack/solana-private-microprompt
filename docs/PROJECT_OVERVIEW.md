# Project Overview

## Working title
Solana Paid Leaderboard (Dream Sheep Jump)

## Product shape
- **Local leaderboard (free):** instant local storage and display.
- **Global leaderboard (paid):** score publication requires fee and on-chain update.

## MVP statement (explicit)
MVP is a **paid publication layer** for scores, not a full anti-cheat system.

### MVP includes
1. Local game session + local score handling.
2. Wallet-connected `submit_score` transaction.
3. Fee transfer + score update behavior.
4. On-chain `PlayerScore`-style state for best score per player.
5. Global leaderboard derived from chain state.

### MVP excludes
1. Verified game binary attestation.
2. Cryptographically linked per-action session logs on-chain.
3. Replay-based score adjudication.
4. zk/zkVM proof validation for score correctness.

## Why best-score-per-player
- Reduces account growth and rent exposure.
- Simplifies leaderboard query and sorting.
- Fits hackathon constraints while still proving on-chain integrity.

## Why no per-action on-chain logging in MVP
- Too expensive/noisy for high-frequency game actions.
- Introduces major complexity and UX latency.
- Not required to demonstrate paid global publication + chain source-of-truth.

## Roadmap direction
- Session/channel ID per run.
- Optional pre-session integrity assertion/attestation.
- Hash-linked action records and transcript commitments.
- Optional verification layer and verified-run badges.
