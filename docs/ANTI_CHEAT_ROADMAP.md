# Future Anti-Cheat Architecture (Roadmap, Non-MVP)

> This section is conceptual architecture only. It is intentionally out of current MVP scope.

## 1) Goals
Increase confidence that a published score came from a valid game run.

## 2) Session/channel model
Each run is represented by a unique `session_id`.

Potential lifecycle:
1. `start_session(session_id, player, game_id, metadata_commitment)`
2. local gameplay emits ordered action records
3. action transcript commitment is sealed
4. score submission references session commitment
5. optional verifier classifies run as verified/unverified

## 3) Pre-session integrity idea
Before gameplay starts, future versions may include integrity evidence (for example attestation metadata), enabling stronger confidence in untampered client/runtime context.

## 4) Action transcript concept
Each record can include:
- `session_id`
- monotonic counter
- logical/game timestamp
- action payload hash
- previous record hash
- record hash

This creates a hash-linked transcript chain suitable for replay/audit pipelines.

## 5) Commitment layer
Instead of storing all actions on-chain:
- maintain transcript off-chain,
- store periodic or final commitment root on-chain,
- verify transcript consistency against root when needed.

## 6) Verification tiers
- **Tier 0 (MVP):** no run-proof verification.
- **Tier 1:** session commitment checks and consistency rules.
- **Tier 2:** replay/audit validator for suspicious runs.
- **Tier 3:** optional zk/zkVM proof-backed verification and badge issuance.

## 7) Verified badge concept
Future leaderboard entries can include trust classes:
- `published` (MVP default)
- `verified_session` (commitment checks passed)
- `proof_verified` (advanced verifier/proof passed)

## 8) Why this is deferred
- Significant complexity and cost.
- Requires dedicated correctness models for game rules.
- Not required for demonstrating paid on-chain publication integrity in MVP.
