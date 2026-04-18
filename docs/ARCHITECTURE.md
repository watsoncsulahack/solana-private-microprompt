# Architecture

## 1) System context
- **Buyer** defines a purchase policy.
- **Wallet** signs policy creation and funding/authorization transactions.
- **Checkout Agent** watches for availability and attempts purchase within policy bounds.
- **Merchant / Demo Drop Service** represents the time-sensitive purchase target.
- **Anchor program** enforces policy + receipt rules.
- **On-chain PDAs** persist policy and receipt source-of-truth.
- **Frontend/API** reads chain state and renders policies and receipts.

(See `docs/diagrams/system-context.md`.)

## 2) Architectural rationale

### Why Solana for delegated checkout
- Fast confirmation and low fees fit time-sensitive authorization flows.
- Publicly auditable policy state and receipt history.
- Easy explorer-based demo proof for judges.

### Why Anchor
- Faster development with typed account constraints.
- Cleaner account validation and instruction handling.
- IDL-driven client integration.

### Why PDAs
- Deterministic account addresses for per-policy and per-receipt state.
- No private key required for program-owned account derivation.
- Natural fit for `(authority, merchant_id, item/window)` policy records.

### Why bounded policy state on-chain
- Lower risk than unrestricted delegated keys.
- Enough to prove what the user allowed and what the agent executed.
- Avoids pretending Solana is the full commerce engine.

## 3) Current trust boundary
- **Trusted for MVP:** on-chain authorization integrity, receipt integrity, and bounded policy enforcement.
- **Not yet trust-minimized:** external merchant fulfillment, generalized web automation, and agent behavior outside the authorized transaction flow.

## 4) Current-state flow
1. Buyer creates a purchase policy.
2. Buyer funds or authorizes a capped spend.
3. Checkout agent monitors a demo drop or mock merchant.
4. Agent executes purchase if conditions fit policy.
5. Program validates policy constraints and records receipt.
6. Frontend reads chain state and renders policy + receipt status.

## 5) Why universal merchant automation is deferred
- Real merchant ecosystems vary widely.
- Safe checkout automation requires careful scope and consent controls.
- Hackathon objective is clear bounded-authorization integrity first.

## 6) Future delegated-checkout architecture (non-MVP)
- Merchant-specific adapters.
- Signed merchant callbacks or webhook reconciliation.
- Delegated session keys or scoped execution rights.
- Better order-status state machines and refund flows.
- Optional attestations for agent runs.

Detailed roadmap: `docs/ANTI_CHEAT_ROADMAP.md`.

## 7) Open implementation gaps (code)
- Program implementation of Config PDA, PurchasePolicy PDA, and PurchaseReceipt PDA.
- Instruction handlers and account constraints in Anchor.
- Wallet/policy UX and tx confirmation states.
- Demo merchant or mocked drop integration.
