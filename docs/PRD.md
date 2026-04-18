# Product Requirements Document (PRD)

## 1. Problem
Arcade-style games need globally trusted scoreboards. Pure client-side leaderboards are easy to spoof, and centralized DB-only boards are opaque.

## 2. Product Vision
A two-tier leaderboard:
- **Local (free)** for instant user feedback.
- **Global (paid + on-chain)** for verifiable, monetized competitive ranking.

## 3. Goals (MVP)
1. Enforce a micro-payment before global score submission.
2. Persist global score records on Solana devnet.
3. Reconstruct top scores from on-chain data only.
4. Keep local leaderboard fully usable without wallet/payment.

## 4. Non-Goals (MVP)
- Full anti-cheat cryptographic guarantees.
- Mainnet deployment.
- Multi-game economy.
- Tournament matchmaking.

## 5. Personas
- **Player**: wants fast local play and optional global competition.
- **Competitive player**: pays for globally visible ranking.
- **Judge**: needs clear proof that global board entries are paid and on-chain.

## 6. User Stories
- As a player, I can save local scores for free.
- As a player, I can connect wallet and pay to submit a global score.
- As a player, I can view global top scores derived from chain data.
- As an operator, I can verify each global score with tx signatures.

## 7. MVP Features
- Wallet connect + devnet flow.
- Submit score instruction with payment gate.
- On-chain score accounts.
- Leaderboard reader/indexer API.
- Local leaderboard storage and UI.

## 8. Success Metrics
- >= 5 successful paid submissions in demo window.
- Global top 10 reproducible from chain scan.
- End-to-end submission (wallet->tx->leaderboard) under 60s median.

## 9. Risks
- RPC reliability and latency.
- Wallet UX friction on mobile.
- Spoofed client scores in MVP (known limitation).

## 10. Anti-cheat Positioning
- MVP: integrity of payment + recording, not score authenticity.
- Future: session commitments + optional ZK proof-based validation.
