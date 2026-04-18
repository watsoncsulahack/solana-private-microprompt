# Software Requirements Document (SRD)

## 1. System Context
This project combines client-side gameplay with on-chain publication:
- gameplay state is local,
- publication state is on-chain.

## 2. Technology Choices
- **Chain**: Solana Devnet
- **Program framework**: Anchor (Rust)
- **Client**: web/mobile-web game UI
- **Leaderboard read path**: chain scan via indexer/API

## 3. On-chain Data Model (MVP)

### Account: `PlayerBestScore`
Recommended PDA seeds:
- `b"best_score"`
- `game_id`
- `player_pubkey`

Fields:
- `game_id: String`
- `player: Pubkey`
- `best_score: u32`
- `best_score_submitted_at: i64`
- `total_paid_lamports: u64`
- `submit_count: u32`
- `last_tx_ref: [u8; 64]` (or signature string)
- `session_commitment: [u8; 32]` (reserved; optional in MVP)

## 4. Instruction Contract (MVP)

### `submit_score(game_id, score)`
Atomic behavior:
1. Validate signer and account constraints.
2. Validate payment transfer rule to treasury (in same transaction/ix flow).
3. Create/update `PlayerBestScore` PDA.
4. Update `best_score` only if new score is higher.
5. Increment `submit_count`; track paid totals.

## 5. Functional Requirements
- FR1: local score save must not touch chain.
- FR2: global submission requires successful payment check.
- FR3: global score write must be deterministic and idempotent-safe.
- FR4: leaderboard API must derive ranking from on-chain records only.

## 6. Non-Functional Requirements
- NFR1: mobile-friendly latency for submit path.
- NFR2: deterministic sorting (score desc, then earliest timestamp).
- NFR3: clear failure diagnostics for wallet/payment/RPC errors.

## 7. API Surface (supporting services)
- `GET /leaderboard/global?gameId=&limit=`
- `GET /leaderboard/global/latest?gameId=`
- `GET /leaderboard/local` (client-only)

Note: API is read/index convenience, not source of truth.

## 8. Trust Model (MVP)
- Trusts client-reported score with basic sanity checks.
- Trusts chain for payment + publication integrity.
- Does not prove run legitimacy.

## 9. Future Verification Layer (non-MVP)
- session/channel start event
- monotonic action counter and hash-chain links
- optional commitment tree or transcript root
- optional proof verifier pathway (zk/zkVM)

## 10. Rationale for Best-Score-per-Player Pattern
- Lower account growth and easier indexing than per-run accounts.
- Better user experience for “global best” board.
- Can be extended later with per-run optional logs if needed.
