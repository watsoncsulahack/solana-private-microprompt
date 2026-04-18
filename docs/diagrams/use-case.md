# UML Use Case Diagram (Mermaid)

```mermaid
flowchart LR
  Buyer((Buyer))
  Agent((Checkout Agent))
  Admin((Admin))
  Wallet((Wallet))
  Chain((Solana Devnet))
  Merchant((Demo Merchant))
  API((Policy / Receipt API))

  subgraph MVP[Current MVP]
    U1([Create purchase policy])
    U2([Fund or authorize capped budget])
    U3([Connect wallet])
    U4([Execute delegated purchase])
    U5([Enforce price/quantity/expiry limits])
    U6([Cancel policy])
    U7([View policy and receipt status])
    U8([Update config state])
  end

  subgraph FUTURE[Future / Non-MVP]
    F1([Start execution session])
    F2([Record audit transcript])
    F3([Reconcile with merchant callback])
    F4([View attested receipt])
  end

  Buyer --> U1 --> Wallet --> Chain
  Buyer --> U2 --> Wallet --> Chain
  Buyer --> U3 --> Wallet
  Agent --> U4 --> Merchant
  U4 --> U5 --> Chain
  Buyer --> U6 --> Wallet --> Chain
  Buyer --> U7 --> API --> Chain
  Admin --> U8 --> Chain

  Agent -. roadmap .-> F1 --> F2 --> F3 --> F4
```
