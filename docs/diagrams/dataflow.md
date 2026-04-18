# Dataflow Diagram (Mermaid)

```mermaid
flowchart TD
  A[Dream Sheep Jump Client] -->|Local score event| B[Local Storage]
  A -->|Connect + sign tx| C[Wallet]
  C -->|submit_score tx| D[Anchor Program]
  D -->|write/update PlayerBestScore PDA| E[Solana Devnet]

  F[Indexer/API] -->|scan best-score accounts| E
  F -->|top-N leaderboard| A

  subgraph Future Anti-Cheat Channel (Non-MVP)
    G[start_session]
    H[Action Transcript Hash Chain]
    I[Session Commitment Root]
    J[Optional Verifier (zk/zkVM)]
  end

  A -. roadmap .-> G
  A -. roadmap .-> H
  H -. roadmap .-> I
  I -. roadmap .-> J
  J -. roadmap .-> D
```
