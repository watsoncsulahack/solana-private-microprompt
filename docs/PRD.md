# Product Requirements Document (PRD)

## 1) Problem
People routinely miss time-sensitive purchase windows because manual checkout is slow, fragile, and hard to coordinate across devices. Existing automation is often unsafe because it requires broad account or payment access.

## 2) Vision
A Solana-backed delegated checkout system where a user can pre-authorize a narrow purchase policy and allow an agent to execute that purchase on their behalf within strict limits.

## 3) MVP goals
1. Let a user create a constrained purchase policy.
2. Allow a delegated agent to execute a purchase only inside that policy.
3. Record policy state and purchase receipts on-chain.
4. Show a clear audit trail of what the agent was allowed to do and what it actually did.

## 4) Non-goals (MVP)
- Beating anti-bot systems.
- Mass-scalping scarce inventory.
- Unrestricted wallet delegation.
- Full merchant ecosystem integration.
- Mainnet launch.

## 5) Personas
- **Buyer:** wants help completing a time-sensitive purchase without giving away full wallet control.
- **Agent operator:** wants a narrow, machine-readable policy it can safely execute.
- **Judge/reviewer:** needs clear proof that the agent acted within user-defined limits.
- **Merchant/demo operator:** wants a safe constrained purchase flow rather than an adversarial bot.

## 6) Core user stories
- Create a purchase policy with merchant/item/price/quantity/time limits.
- Fund or authorize that policy from a wallet.
- Let an agent monitor and execute the purchase when conditions are met.
- See whether a policy is active, executed, expired, or cancelled.
- View a purchase receipt and policy audit trail.

## 7) MVP feature set
- Wallet integration for policy creation.
- On-chain `PurchasePolicy` account.
- Agent-triggered `execute_purchase` flow.
- On-chain `PurchaseReceipt` account.
- Policy status UI and receipt viewer.

## 8) Assumptions and constraints
- MVP may use a controlled merchant demo, mocked drop page, or ticketing-style checkout simulator.
- Solana is the authorization/payment/audit layer, not the full commerce backend.
- The delegated agent is trusted to follow the program and off-chain integration rules, but its authority is bounded by on-chain policy state.
- Policy evaluation should remain understandable to non-expert judges.

## 9) Risks and tradeoffs
- **Fast hackathon scope vs broad merchant coverage:** choose one demo integration or mock merchant.
- **Delegation convenience vs wallet safety:** choose explicit caps and expiry windows.
- **On-chain transparency vs external order ambiguity:** store policy and receipt references, not full merchant internals.
- **Safe positioning vs flashy “sniping” language:** choose user-authorized checkout framing.

## 10) Success criteria
- Demonstrable end-to-end policy creation on Devnet.
- Agent-triggered execution constrained by policy parameters.
- On-chain receipt proving what was authorized and what was executed.
- Demo understandable in <3 minutes.

## 11) Future direction (non-MVP)
- Merchant integrations and webhooks.
- Partial fills / retries.
- Refund handling.
- Delegated session keys.
- Trusted merchant attestations and richer receipts.
