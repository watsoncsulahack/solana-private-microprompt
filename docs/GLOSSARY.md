# Glossary

- **Player**: End user playing the game.
- **Wallet**: Solana wallet used to sign submission transactions.
- **Local Game Session**: Client-side gameplay run not committed on-chain in MVP.
- **Score**: Numeric result from one gameplay run.
- **Best Score**: Highest published score for a player/game pair.
- **Score Submission**: Transaction flow that publishes score globally.
- **Submission Fee**: Required payment to publish a global score.
- **Local Leaderboard**: Free local ranking stored on device/browser.
- **Global Leaderboard**: Ranking reconstructed from on-chain score state.
- **Config State / Config PDA**: Program-owned configuration account (fee, admin, pause, treasury).
- **PlayerScore Account / PDA**: Program-owned per-player best-score account.
- **Future Verified Session**: Roadmap concept for stronger run validation.
- **Future Action Transcript / Hash Chain**: Roadmap concept for cryptographically linked action logs.
- **Anchor**: Rust framework for Solana programs with account validation + IDL.
- **PDA**: Program Derived Address, deterministic program-owned account address.
