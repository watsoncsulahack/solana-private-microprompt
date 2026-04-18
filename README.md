# Solana Private MicroPrompt

Pay-per-prompt local AI inference on a mobile device.

## Concept
Users submit prompts and pay a micro-transaction on Solana devnet. After payment verification, a local on-device model processes the prompt and returns a response.

## Core Value
- **Privacy-first**: no cloud inference required.
- **Micropayments**: per-prompt pricing on Solana.
- **Agent-ready**: compatible with autonomous agent workflows.

## Scope (Hackathon MVP)
- Devnet only.
- Single model host (phone/device) online during demo.
- Payment gate + inference API + lightweight web UI.
- Basic observability and anti-abuse controls.

## Documentation
- Product Requirements: `docs/PRD.md`
- Software Requirements: `docs/SRD.md`
- UML / architecture diagrams: `docs/diagrams/*.md`
