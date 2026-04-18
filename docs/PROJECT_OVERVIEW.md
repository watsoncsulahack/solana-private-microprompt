# Project Overview

## Working Title
Solana Paid Leaderboard (Dream Sheep Jump)

## One-liner
A game leaderboard where local scores are free, but global score submissions require a Solana devnet micro-payment and are stored on-chain.

## Core Product Shape
1. Play game locally.
2. Save free local score.
3. Pay micro-fee to submit to global board.
4. Write score record on-chain.
5. Rebuild global top rankings from chain data.

## Why this is strong for hackathon
- Clear user value and clear business model.
- Easy to demo in <3 minutes.
- Verifiable by tx signatures and explorer links.
- Expandable to anti-cheat research direction.

## Anti-cheat roadmap
### MVP (now)
- Basic sanity checks only (bounds, timestamp windows).

### V1.5
- Session start commitment on-chain.
- Submit score with signed session evidence.

### V2 (research)
- ZK proof of valid run constraints (inspiration: ZK Battleships-style proof framing).

## Deliverables for submission
- On-chain score program (Anchor)
- Web client with wallet + submit flow
- Local leaderboard + global leaderboard views
- Indexer/API to read global leaderboard from chain
- Demo script + architecture docs
