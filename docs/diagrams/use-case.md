# UML Use Case Diagram (Mermaid)

```mermaid
flowchart LR
  Player((Player))
  Wallet((Wallet))
  Chain((Solana Devnet))
  API((Leaderboard API))

  subgraph MVP[Current MVP]
    UC1([Play Game])
    UC2([Save Local Score - Free])
    UC3([Connect Wallet])
    UC4([Pay + Submit Global Score])
    UC5([Program Validates Payment])
    UC6([Update Best Score PDA])
    UC7([View Global Leaderboard])
  end

  subgraph FUTURE[Future Verification Layer - Non-MVP]
    UC8([Start Session Channel])
    UC9([Generate Hash-linked Action Transcript])
    UC10([Submit Session Commitment])
    UC11([Optional Proof Verification])
    UC12([Verified-Run Badge])
  end

  Player --> UC1 --> UC2
  Player --> UC3 --> Wallet
  Player --> UC4 --> Wallet --> Chain
  UC4 --> UC5 --> UC6 --> Chain
  Player --> UC7 --> API --> Chain

  Player -. roadmap .-> UC8 --> UC9 --> UC10
  UC10 -. roadmap .-> UC11 --> UC12
```
