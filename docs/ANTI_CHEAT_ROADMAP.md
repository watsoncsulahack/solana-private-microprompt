# Anti-Cheat Roadmap (Future Architecture)

> This document is explicitly **non-MVP**.

## 1. Objective
Improve confidence in score legitimacy beyond payment/publication integrity.

## 2. Session / Channel Concept
A run is modeled as a unique `session_id` channel.

### Session lifecycle (future)
1. `start_session(session_id, game_id, player, commitment_meta)`
2. gameplay actions generate transcript entries
3. `end_session(session_id, final_commitment, score)`
4. optional verifier checks transcript constraints

## 3. Transcript Structure (future)
Each entry may include:
- `session_id`
- `counter` (monotonic)
- `action_type`
- `action_payload_hash`
- `prev_hash`
- `entry_hash`

This forms a hash-linked chain of gameplay events.

## 4. Commitment Strategies
- Simple rolling hash commitment.
- Merkle-root commitment over batched events.
- Periodic checkpoint roots.

## 5. Verification Tiers
### Tier 0 (MVP today)
No cryptographic run validity proof.

### Tier 1
Session commitments + consistency checks.

### Tier 2
External attestation inputs (where feasible).

### Tier 3
Proof-based verification (zk/zkVM) for selected constraints.

## 6. Example Constraints for Future Proofing
- monotonic score progression bounds
- valid jump timing windows
- impossible physics transition rejection
- no retroactive event insertion

## 7. Practical Positioning
For hackathon and early versions:
- avoid claiming “cheat-proof”
- claim “on-chain publication integrity”
- present anti-cheat as an active roadmap with concrete architecture hooks already reserved
