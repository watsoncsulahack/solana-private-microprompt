# Project Overview

## Working Title
Solana Private MicroPrompt

## One-liner
A devnet app where users pay a micro-transaction per prompt, then a local phone-hosted model processes the request privately.

## Why this project
- Demonstrates practical AI monetization on Solana.
- Showcases local/on-device inference utility.
- Strong hackathon demo story with clear transaction proof.

## MVP Boundary
- Devnet only
- Single local host
- Minimal persistence (metadata only)
- Focus on reliability and demo clarity

## Immediate Next Build Tasks
1. Scaffold web UI and wallet connect flow.
2. Implement payment verification endpoint.
3. Add entitlement token issuance + one-time use.
4. Wire inference endpoint to local runtime.
5. Add demo telemetry panel (request state + tx links).
