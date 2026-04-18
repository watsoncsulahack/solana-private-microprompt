# Project Overview

## Working Title
Solana Paid Leaderboard (Dream Sheep Jump)

## One-liner
A two-tier leaderboard: local scores are free, while global scores require Solana payment and are persisted on-chain.

## Scope Boundary (critical)

### MVP includes
- Local score tracking and local leaderboard.
- Wallet flow for paid global submission.
- On-chain best-score-per-player storage.
- Leaderboard reconstruction from chain records.

### MVP excludes
- Full anti-cheat proof of score validity.
- Session transcript verification.
- zk/zkVM score proofs.
- Binary attestation.

## Core assumptions
- Devnet only for hackathon phase.
- Client score input is accepted with basic sanity checks.
- Payment and publication integrity are the trust anchors in MVP.

## Why this is presentation-ready
- It demonstrates monetization + verifiability.
- It has clear architecture evolution paths.
- It avoids overclaiming anti-cheat in MVP.

## Architecture evolution model

### Phase 0 (MVP)
Paid score publication + chain-sourced leaderboard.

### Phase 1 (near-term)
Session start marker + stronger submission constraints.

### Phase 2 (research)
Session/channel cryptographic transcript and optional proof verification.

## Deliverables for hackathon submission
1. On-chain score program (Anchor)
2. Frontend game + wallet submit flow
3. Global leaderboard view sourced from chain
4. Documentation package (requirements + diagrams + roadmap)
