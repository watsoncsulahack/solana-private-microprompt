# Data Flow Diagram (Mermaid)

```mermaid
flowchart TD
  A[Buyer App] -->|Create purchase policy| B[Wallet Adapter]
  B -->|Signed tx| C[Anchor Program: create_policy]
  C -->|Read rules| D[(Config PDA)]
  C -->|Create policy| E[(PurchasePolicy PDA)]

  F[Delegated Checkout Agent] -->|Watch availability| G[Demo Merchant / Drop Service]
  F -->|Execute within policy| H[Anchor Program: execute_purchase]
  H -->|Read policy constraints| E
  H -->|Service fee / authorized spend path| I[(Treasury or Budget Flow)]
  H -->|Create immutable receipt| J[(PurchaseReceipt PDA)]
  H -->|Update policy status| E

  K[Policy / Receipt API] -->|Fetch policy + receipts| E
  K -->|Fetch receipts| J
  K -->|Return statuses| L[Buyer Dashboard]

  subgraph Future reconciliation path (Non-MVP)
    M[start_execution_session]
    N[Integration event log]
    O[Hash-linked audit transcript]
    P[Merchant callback / attestation]
  end

  F -. roadmap .-> M -.-> N -.-> O -.-> P
  P -. roadmap .-> J
```
