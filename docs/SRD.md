# Software Requirements Document (SRD)

## 1) Stack
- Solana Devnet
- Anchor program (Rust)
- Web/mobile-web game client
- Optional indexer/API for leaderboard read convenience

## 2) Domain model (current)
- `ConfigState` (program config and fee settings)
- `PlayerScore` (best score per player per game)
- Local game session (client-side only)
- Score submission event (wallet tx)

## 3) On-chain accounts (MVP)

### Config PDA
Purpose: global configuration for a game/leaderboard program instance.

Suggested fields:
- `admin: Pubkey`
- `treasury: Pubkey`
- `submission_fee_lamports: u64`
- `game_id: String`
- `is_paused: bool`
- `bump: u8`

### PlayerScore PDA
Purpose: one account per `(game_id, player)` storing best published score.

Suggested fields:
- `game_id: String`
- `player: Pubkey`
- `best_score: u32`
- `best_score_submitted_at: i64`
- `submit_count: u32`
- `total_paid_lamports: u64`
- `last_submit_sig_ref: [u8; 64]` (optional helper)
- `session_commitment: [u8; 32]` (reserved for roadmap)
- `bump: u8`

## 4) Instruction behavior (MVP)

### `submit_score(score: u32, game_id: String)`
Required behavior:
1. Read/validate Config PDA.
2. Enforce pause rules and score sanity bounds.
3. Transfer submission fee to treasury in the same transaction flow.
4. Create/update PlayerScore PDA.
5. If `score > best_score`, overwrite best-score fields.
6. If score is non-improving, preserve best score but still record attempt/payment metrics as designed.

### `update_config(...)` (admin, optional but recommended)
- Update fee, treasury, pause flag, etc.
- Admin-only.

## 5) Why atomic flow matters
Fee transfer and score update should be part of one coherent transaction path to avoid:
- paid but unpublished submissions,
- unpublished fee ambiguity,
- inconsistent leaderboard state.

## 6) Leaderboard query model
Global leaderboard read path:
1. Fetch all `PlayerScore` PDAs for `game_id`.
2. Sort by:
   - `best_score` descending,
   - `best_score_submitted_at` ascending,
   - `player` lexicographic as deterministic tie-break.
3. Return top-N.

## 7) Client publication semantics
- Local scores are marked unpublished until a successful on-chain submit is confirmed.
- Published status is tied to tx confirmation + updated PlayerScore readback.

## 8) Non-functional notes
- Devnet latency/resilience constraints are expected.
- Keep transaction count low (best-score model).
- Avoid large account growth in MVP.

## 9) Roadmap hooks (non-MVP)
- `session_commitment` field reserved for transcript root.
- Future instructions: `start_session`, `close_session`, `submit_transcript_commitment`.
- Future verifier adapter for proof-backed run classification.
