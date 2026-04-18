# Data Flow Diagram (Mermaid)

```mermaid
flowchart TD
  A[Player/Game Client] -->|Play locally| B[Local score]
  B -->|Save free| C[Local leaderboard store]

  A -->|Connect wallet| D[Wallet Adapter]
  A -->|Submit score request| D
  D -->|Signed tx| E[Anchor Program: submit_score]
  E -->|Read rules| F[(Config PDA)]
  E -->|Fee transfer to treasury| G[(Treasury)]
  E -->|Create/update best score| H[(PlayerScore PDA)]

  I[Leaderboard API/Indexer] -->|Fetch PlayerScore PDAs| H
  I -->|Sort and return top-N| J[Leaderboard UI]

  subgraph Future verification path (Non-MVP)
    K[start_session]
    L[Action records + monotonic counter]
    M[Hash-linked transcript]
    N[Transcript commitment]
    O[Optional verifier/proof adapter]
  end

  A -. roadmap .-> K -.-> L -.-> M -.-> N -.-> O
  O -. roadmap .-> E
```
