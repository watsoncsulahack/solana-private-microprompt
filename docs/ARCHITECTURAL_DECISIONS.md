# Architectural Decision Notes

## ADR-001: Paid global submission model
**Decision:** Require fee for global leaderboard publication.
**Reason:** Spam resistance + clear economic signal for global rank.

## ADR-002: Best-score-per-player on-chain
**Decision:** Store only player best score for MVP.
**Reason:** Lower cost, cleaner indexing, fast leaderboard queries.

## ADR-003: Anchor + PDA account model
**Decision:** Use Anchor and PDA-derived account state.
**Reason:** Deterministic account ownership, safer account constraints, faster development.

## ADR-004: Keep gameplay execution client-side
**Decision:** Do not run gameplay on-chain.
**Reason:** Throughput/cost mismatch for high-frequency game actions.

## ADR-005: Anti-cheat deferred to roadmap
**Decision:** Treat anti-cheat as future cryptographic verification layer.
**Reason:** Substantial complexity not required for MVP publication integrity demo.
