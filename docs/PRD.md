# Product Requirements Document (PRD)

## 1) Problem
Players want globally visible high scores with stronger integrity than a local or opaque centralized leaderboard.

## 2) Vision
A paid global leaderboard where each published score is tied to an on-chain Solana transaction.

## 3) MVP goals
1. Free local gameplay and local leaderboard.
2. Paid global score submission.
3. On-chain best-score-per-player state.
4. Global ranking reconstructed from chain data.

## 4) Non-goals (MVP)
- Full anti-cheat/tamper-resistance.
- Per-action on-chain run logs.
- zk score validity proofs.
- Mainnet launch.

## 5) Personas
- **Player:** wants fast play and optional global rank.
- **Competitive player:** willing to pay to publish rank.
- **Judge/reviewer:** needs clear, verifiable architecture and realistic scope.

## 6) Core user stories
- Save local score without wallet.
- Connect wallet and submit global score.
- Pay submission fee and receive confirmation.
- View global leaderboard sourced from chain state.
- See whether score was unpublished (local) or published (global).

## 7) MVP feature set
- Local score capture and local board UI.
- Wallet integration for `submit_score`.
- On-chain program update of best score.
- Leaderboard API/client sort path.

## 8) Assumptions and constraints
- Client-generated scores are trusted in MVP.
- Global leaderboard integrity is on-chain.
- Gameplay integrity is not fully enforced yet.
- Blockchain is publication/source-of-truth layer, not full game execution layer.

## 9) Risks and tradeoffs
- **Simple MVP vs strong anti-cheat:** chose MVP simplicity now.
- **On-chain permanence vs storage cost:** store best-score only.
- **Transparency vs cost:** avoid per-action logs in MVP.
- **Client simplicity vs cryptographic assurance:** roadmap handles stronger verification later.

## 10) Success criteria
- Demonstrable paid global submissions on Devnet.
- Top-N leaderboard reproducible from on-chain state.
- End-to-end demo flow understandable in <3 minutes.

## 11) Future anti-cheat direction (non-MVP)
- Session/channel start + session ID.
- Hash-linked action transcript.
- Optional attestation/proof adapters.
- Verified-run badge tier for stronger trust classes.
