# Future Delegated-Checkout Roadmap (Roadmap, Non-MVP)

> This section is conceptual architecture only. It is intentionally out of current MVP scope.

## 1) Goals
Increase confidence that delegated purchases are executed safely, transparently, and with better merchant interoperability.

## 2) Agent session model
Each delegated purchase attempt can be represented by a unique `execution_session_id`.

Potential lifecycle:
1. `start_execution_session(policy_id, agent_ref, metadata_commitment)`
2. agent watches availability and prepares checkout
3. agent attempts execution within policy bounds
4. purchase outcome is reconciled with merchant/demo service
5. optional attestation or webhook evidence is attached to receipt

## 3) Pre-execution integrity idea
Before execution starts, future versions may include stronger agent identity or attestation metadata, enabling more confidence in which automation stack acted under the policy.

## 4) Action/audit transcript concept
Each record can include:
- `execution_session_id`
- monotonic counter
- logical timestamp
- request/response metadata hash
- previous record hash
- record hash

This creates a hash-linked transcript suitable for audit pipelines.

## 5) Commitment layer
Instead of storing every integration event on-chain:
- maintain transcript off-chain,
- store periodic or final commitment root on-chain,
- verify transcript consistency against root when needed.

## 6) Verification tiers
- **Tier 0 (MVP):** bounded on-chain policy + receipt only.
- **Tier 1:** execution session metadata and consistency checks.
- **Tier 2:** merchant reconciliation or signed callback verification.
- **Tier 3:** optional attested agent execution / richer proofs.

## 7) Future trust classes
Future receipts can include trust classes:
- `policy_recorded` (MVP default)
- `session_recorded` (execution metadata captured)
- `merchant_reconciled` (merchant callback confirmed)
- `attested_execution` (advanced attestation passed)

## 8) Why this is deferred
- Significant complexity and integration work.
- Merchant-specific requirements vary widely.
- Not required for demonstrating bounded delegated payment authorization in MVP.
