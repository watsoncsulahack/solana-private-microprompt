# UML Use Case Diagram (Mermaid)

```mermaid
flowchart LR
  Player((Player))
  Wallet((Wallet))
  Chain((Solana Devnet))
  API((Leaderboard API))

  subgraph System[Paid Global Leaderboard]
    UC1([Play Game])
    UC2([Save Local Score - Free])
    UC3([Connect Wallet])
    UC4([Pay + Submit Global Score])
    UC5([Program Validates Payment])
    UC6([Store Score On-chain])
    UC7([View Global Leaderboard])
  end

  Player --> UC1 --> UC2
  Player --> UC3
  UC3 --> Wallet
  Player --> UC4
  UC4 --> Wallet --> Chain
  UC4 --> UC5 --> UC6 --> Chain
  Player --> UC7 --> API --> Chain
```
