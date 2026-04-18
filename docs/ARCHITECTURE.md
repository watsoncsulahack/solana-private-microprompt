# Architecture Deep Dive

## 1. System Layers

### Layer A: Gameplay (Local, Free)
- Runs game loop and scoring logic locally.
- Stores local leaderboard in browser/device.
- No wallet required.

### Layer B: Publication (Paid, On-chain)
- Wallet signs submit transaction.
- Program enforces payment + score publication rules.
- Best score per player persisted on-chain.

### Layer C: Read Path (Indexed)
- Indexer/API scans chain accounts.
- Frontend renders top-N board from chain-derived records.

## 2. Key Design Decisions

### Decision 1: On-chain source of truth for global board
Reason: enables independent reconstruction and trust-minimized ranking.

### Decision 2: Best-score-per-player account model
Reason: simpler storage/indexing and stronger MVP clarity.

### Decision 3: Atomic payment + score submit
Reason: avoids paid-but-not-published or published-without-payment states.

### Decision 4: Anti-cheat as roadmap, not MVP claim
Reason: realistic delivery scope and technical honesty for hackathon.

## 3. MVP Transaction Sequence
1. Player finishes run locally.
2. Player chooses “Submit Global”.
3. Wallet signs transaction with payment + submit instruction.
4. Program validates and updates player best-score account.
5. API reads chain account updates; frontend leaderboard refreshes.

## 4. Data Integrity Notes
- Ranking determinism should be fixed in one canonical sort order:
  1) score descending
  2) earliest best-score timestamp ascending
  3) player pubkey ascending (stable tie-break)

## 5. Failure Modes and Handling
- Wallet reject: client reports and leaves local score untouched.
- Underpayment: program reject, no write.
- RPC timeout: client retry strategy, no local/global divergence in state claims.
- Duplicate submit: idempotent-safe update logic.

## 6. Security and Abuse (MVP)
- Payment-gated publication reduces spam.
- Basic score bounds/sanity checks mitigate trivial abuse.
- Full score legitimacy not guaranteed (explicitly disclosed).

## 7. Future Cryptographic Verification Layer (non-MVP)
- Session/channel ID created at run start.
- Optional binary integrity attestation reference.
- Action transcript with monotonic counter + hash-linking.
- Transcript commitment (single root) attached at submit.
- Optional verifier for advanced proof modes (zk/zkVM) and “verified run” badges.
