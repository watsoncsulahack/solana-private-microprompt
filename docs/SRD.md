# Software Requirements Document (SRD)

## 1. Architecture Components
1. **Game Client (Web/Mobile Web)**
   - Runs Dream Sheep Jump UI.
   - Manages local score storage.
2. **Wallet + Payment UI**
   - Signs and sends devnet payment/submission tx.
3. **On-chain Program (Anchor)**
   - Validates payment rule.
   - Stores global score record account.
4. **Leaderboard Indexer/API**
   - Reads score accounts from chain.
   - Returns sorted top-N responses.
5. **Local Store**
   - Browser localStorage for local leaderboard.

## 2. Core Data Model (On-chain)
### ScoreSubmission Account
- `game_id: String`
- `player: Pubkey`
- `score: u32`
- `played_at: i64`
- `submitted_at: i64`
- `payment_lamports: u64`
- `tx_sig_ref: String` (optional helper metadata)
- `session_commitment: [u8;32]` (reserved for anti-cheat roadmap)

## 3. Functional Requirements
- FR1: Local score save must not require wallet.
- FR2: Global score submit must require payment rule enforcement.
- FR3: Program must reject invalid/underpaid submissions.
- FR4: API must reconstruct leaderboard from on-chain records.
- FR5: UI must clearly distinguish local vs global leaderboard.

## 4. Non-Functional Requirements
- NFR1: Devnet-compatible and mobile-browser-friendly.
- NFR2: API should return top-100 in <2s (cache allowed).
- NFR3: Deterministic sorting: score desc, then earliest submit.
- NFR4: No private prompt/PII handling required in this project.

## 5. API Draft
- `GET /leaderboard/global?gameId=...&limit=...`
- `GET /leaderboard/local` (client-side)
- `POST /score/local` (client-side)

(Program interaction is direct via wallet tx; backend does not own truth.)

## 6. Security / Integrity Notes
- On-chain payment and score record are trust anchors.
- Client-reported score still spoofable in MVP.
- Future anti-cheat hooks:
  - session start tx
  - signed frame commitments
  - optional zk proof verification pathway

## 7. Anchor usage
Anchor is used to implement the Solana program with typed accounts and IDL-driven clients, reducing integration complexity and speeding hackathon delivery.
