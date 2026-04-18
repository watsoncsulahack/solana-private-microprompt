# Project Overview

## Working title
Solana Delegated Checkout Agent

## Product shape
- **Policy creation (user-controlled):** user defines exact purchase rules.
- **Delegated execution (agent-controlled):** agent may execute checkout only within those rules.
- **Receipt layer (on-chain):** policy state and execution receipts are auditable.

## MVP statement (explicit)
MVP is a **bounded delegated purchase authorization layer** for time-sensitive purchases, not a universal commerce bot and not an anti-bot bypass system.

### MVP includes
1. Wallet-connected policy creation.
2. Constrained spend rules for a time-sensitive purchase.
3. Agent-triggered execution flow within those rules.
4. On-chain policy state and purchase receipt state.
5. Basic status UI for active, executed, expired, and cancelled policies.

### MVP excludes
1. Bypassing merchant anti-bot systems.
2. Unbounded delegated wallet spending.
3. Guaranteed successful checkout at external merchants.
4. Mainnet launch.
5. Universal merchant integrations.

## Why bounded delegation matters
- Users want automation without surrendering full wallet control.
- Time-sensitive purchases fail when checkout is too slow, not always because the user lacks intent or funds.
- Explicit caps improve safety and explainability for judges and users.

## Why no “drop sniper” framing
- The project is about **authorized assisted checkout**, not unfair market capture.
- The system should work through approved flows, mock merchants, event registration, or controlled demos.
- Long-term merchant cooperation is more valuable than adversarial automation.

## Roadmap direction
- Merchant-specific adapters.
- Better order-status reconciliation.
- Budget vaults / refunds.
- Delegated session keys or scoped execution authorities.
- Optional attestations and stronger audit trails for agent actions.
