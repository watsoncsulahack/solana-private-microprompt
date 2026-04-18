# System Context Diagram (Mermaid)

```mermaid
flowchart LR
  Player((Player))
  Game[Game Client\n(Dream Sheep Jump)]
  Wallet[Wallet Adapter]
  Program[Anchor Program]
  Config[(Config PDA)]
  Score[(PlayerScore PDA)]
  ReadPath[Leaderboard Service / Solana Read Adapter]
  UI[Leaderboard UI]

  Player --> Game
  Game --> Wallet
  Wallet --> Program
  Program --> Config
  Program --> Score
  ReadPath --> Score
  UI --> ReadPath
  Player --> UI

  subgraph FutureLayer[Future Session Verification Layer (Non-MVP)]
    Sess[VerifiedSession]
    Transcript[Action Transcript / Hash Chain]
    Verifier[Replay / Proof / Attestation Layer]
  end

  Game -. roadmap .-> Sess
  Sess -. roadmap .-> Transcript
  Transcript -. roadmap .-> Verifier
  Verifier -. roadmap .-> Program
```
