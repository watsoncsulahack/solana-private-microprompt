# Implementation Notes for Contributors

## Current implementation target
- Build Anchor program first: Config PDA + PlayerScore PDA + `submit_score`.
- Build client score submit flow second.
- Add read/index endpoint or direct account scan for leaderboard rendering.

## Suggested program instruction surface
- `initialize_config`
- `update_config` (admin)
- `submit_score`

## Suggested test priorities
1. fee enforcement
2. improving vs non-improving score behavior
3. deterministic leaderboard sort
4. pause-mode behavior

## Data compatibility guidance
- Keep account schema versioned if fields expand.
- Preserve backwards compatibility for leaderboard reads.

## Future-proof hooks
- Keep `session_commitment` reserved in PlayerScore now.
- Add future instructions in additive way to avoid breaking MVP clients.
