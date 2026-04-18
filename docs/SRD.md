# Software Requirements Document (SRD)

## 1) Stack
- Solana Devnet
- Anchor program (Rust)
- Web/mobile-web client
- Delegated checkout agent service
- Optional mock merchant / demo checkout endpoint

## 2) Domain model (current)
- `ConfigState` (program config and fee settings)
- `PurchasePolicy` (user-defined bounded authorization)
- `PurchaseReceipt` (record of agent execution)
- Agent execution session (off-chain)

## 3) On-chain accounts (MVP)

### Config PDA
Purpose: global configuration for the delegated checkout program.

Suggested fields:
- `admin: Pubkey`
- `treasury: Pubkey`
- `service_fee_lamports: u64`
- `is_paused: bool`
- `bump: u8`

### PurchasePolicy PDA
Purpose: one account per policy storing the user’s bounded delegation rules.

Suggested fields:
- `authority: Pubkey`
- `merchant_id: String`
- `item_constraint_hash: [u8; 32]`
- `max_unit_price_lamports: u64`
- `max_total_spend_lamports: u64`
- `quantity_limit: u16`
- `expires_at: i64`
- `status: u8` // active, executed, expired, cancelled
- `funded_amount_lamports: u64` // optional if using deposit model
- `delegate_ref: Pubkey` // optional agent/operator ref
- `bump: u8`

### PurchaseReceipt PDA
Purpose: immutable record of a completed delegated execution.

Suggested fields:
- `policy: Pubkey`
- `buyer: Pubkey`
- `executor: Pubkey`
- `merchant_id: String`
- `external_order_ref_hash: [u8; 32]`
- `unit_price_lamports: u64`
- `quantity: u16`
- `total_paid_lamports: u64`
- `purchased_at: i64`
- `status: u8` // success, failed, cancelled/refunded
- `bump: u8`

## 4) Instruction behavior (MVP)

### `create_policy(...)`
Required behavior:
1. Validate merchant/item/price/quantity/expiry fields.
2. Create PurchasePolicy PDA.
3. Mark policy active.
4. Optionally lock or reference a user-approved budget.

### `execute_purchase(...)`
Required behavior:
1. Read/validate Config PDA and PurchasePolicy PDA.
2. Enforce pause rules, expiry rules, quantity and price bounds.
3. Ensure requested spend is within authorized budget.
4. Transfer service fee and/or authorized spend according to chosen demo model.
5. Create immutable PurchaseReceipt PDA.
6. Update policy status or remaining budget as designed.

### `cancel_policy(...)`
- Authority-only.
- Marks policy cancelled.
- Unlocks/returns unused funds if deposit model is used.

### `update_config(...)` (admin, optional but recommended)
- Update fee, treasury, pause flag, etc.
- Admin-only.

## 5) Why atomic flow matters
Policy validation, fee movement, and receipt creation should be part of one coherent transaction path to avoid:
- spending outside the user’s limits,
- paid but unrecorded execution,
- ambiguous audit trails.

## 6) Query model
Primary read paths:
1. Fetch active PurchasePolicy PDAs for a buyer.
2. Fetch PurchaseReceipt PDAs by buyer or policy.
3. Sort receipts by `purchased_at` descending.
4. Display policy status and linked execution records.

## 7) Client semantics
- Policies are local-draft until a successful on-chain create is confirmed.
- Executed status is tied to tx confirmation + receipt creation.
- Expired or cancelled policies must be visually distinct from active ones.

## 8) Non-functional notes
- Devnet latency/resilience constraints are expected.
- Keep merchant integration surface small for the MVP.
- Prefer one clean demo merchant flow over many partial integrations.
- Policy evaluation must remain auditable and easy to explain.

## 9) Roadmap hooks (non-MVP)
- richer agent identity/session metadata
- merchant attestation references
- delegated session keys / scoped authorities
- refund and retry state machines
