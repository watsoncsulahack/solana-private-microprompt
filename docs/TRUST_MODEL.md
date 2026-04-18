# Trust Model (Lite)

## Trusted today (MVP)
- Solana transaction confirmation and account state.
- Program-enforced fee + score publication flow.
- Deterministic ranking from on-chain score accounts.

## Not fully trusted today
- Client score honesty.
- Runtime/binary integrity of game client.
- Resistance to sophisticated local tampering.

## Threats considered in MVP
- unpaid spam submissions
- duplicate publish attempts
- basic malformed score payloads

## Threats deferred
- fabricated runs from modified clients
- timing spoofing with forged action histories
- advanced replay attacks without transcript verification

## Practical statement
MVP provides **publication integrity** and **verifiable global state**, not complete gameplay integrity.
