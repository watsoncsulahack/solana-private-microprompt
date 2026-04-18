# UML Use Case Diagram (Mermaid)

```mermaid
flowchart LR
  Buyer((Prompt Buyer))
  Host((Host Operator))
  RPC((Solana RPC))
  LLM((Local LLM Runtime))

  subgraph System[Solana Private MicroPrompt]
    UC1([Connect Wallet])
    UC2([Get Prompt Quote])
    UC3([Pay on Devnet])
    UC4([Verify Payment])
    UC5([Submit Prompt])
    UC6([Run Local Inference])
    UC7([Return Response + Tx Ref])
    UC8([Start/Stop Runtime])
  end

  Buyer --> UC1 --> UC2 --> UC3 --> UC4 --> UC5 --> UC7
  UC4 --> RPC
  UC5 --> UC6 --> LLM
  Host --> UC8
```
