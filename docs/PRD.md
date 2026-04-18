# Product Requirements Document (PRD)

## 1. Problem
Game leaderboards are either:
- easy to spoof (client-only), or
- opaque and centralized (server DB only).

We need a leaderboard that is globally verifiable, while keeping gameplay fast and local.

## 2. Product Vision
A paid global leaderboard where publication requires Solana micro-payment and score records are written on-chain.

## 3. Goals (MVP)
1. Enable free local play and local ranking.
2. Require payment for global score publication.
3. Persist global score records on-chain.
4. Rebuild top rankings using on-chain data only.

## 4. Non-Goals (MVP)
- Definitive anti-cheat prevention.
- zk proof correctness for each run.
- Full game-event transcript verification.
- Mainnet economic tuning.

## 5. Personas
- **Casual player**: wants quick local progression.
- **Competitive player**: wants globally visible ranked score.
- **Judge/reviewer**: wants clear verifiable flow and technical honesty.

## 6. Key User Stories
- As a player, I can play and save local scores with no wallet.
- As a player, I can connect wallet and pay to submit global score.
- As a player, I can view global top scores sourced from chain data.
- As a judge, I can verify submission tx and ranking derivation path.

## 7. MVP Feature Set
- Local leaderboard (browser/device storage)
- Wallet connect (Devnet)
- Paid global submission transaction
- On-chain best-score-per-player record
- Global leaderboard API/UI from chain scans

## 8. Success Metrics
- >= 5 successful paid global submissions in demo.
- Global top 10 reproducible from chain data.
- End-to-end publish flow median under 60 seconds.

## 9. Product Risks
- RPC instability/rate limits.
- Mobile wallet friction.
- Score spoofing (known MVP limitation).

## 10. Mitigations
- Show explicit “MVP trust model” in UI/docs.
- Basic score sanity constraints in program/client.
- Reserve account fields for future anti-cheat commitments.

## 11. Future Product Direction (non-MVP)
- Session/channel model per run.
- Binary attestation hooks.
- Cryptographically linked action transcripts.
- Verified-run badge tier with stronger proof requirements.
