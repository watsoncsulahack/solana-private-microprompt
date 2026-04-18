# System Context Diagram (Mermaid)

```mermaid
flowchart LR
  Buyer((Buyer))
  App[Buyer App]
  Wallet[Wallet Adapter]
  Agent[Delegated Checkout Agent]
  Merchant[Demo Merchant / Drop Service]
  Program[Anchor Program]
  Config[(Config PDA)]
  Policy[(PurchasePolicy PDA)]
  Receipt[(PurchaseReceipt PDA)]
  ReadPath[Policy / Receipt Read Adapter]
  UI[Status UI]

  Buyer --> App
  App --> Wallet
  Wallet --> Program
  Agent --> Merchant
  Agent --> Program
  Program --> Config
  Program --> Policy
  Program --> Receipt
  ReadPath --> Policy
  ReadPath --> Receipt
  UI --> ReadPath
  Buyer --> UI

  subgraph FutureLayer[Future Merchant Reconciliation Layer (Non-MVP)]
    Sess[ExecutionSession]
    Transcript[Audit Transcript / Hash Chain]
    Reconcile[Merchant Callback / Attestation Layer]
  end

  Agent -. roadmap .-> Sess
  Sess -. roadmap .-> Transcript
  Transcript -. roadmap .-> Reconcile
  Reconcile -. roadmap .-> Receipt
```
