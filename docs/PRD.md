# Product Requirements Document (PRD)

## 1. Problem
Users need private AI inference without sending prompts to cloud LLM providers, while enabling simple monetization for inference hosts.

## 2. Product Vision
A "micro transaction prompting" platform where users pay per prompt on Solana devnet and receive responses from a local model host.

## 3. Goals
1. Demonstrate end-to-end payment-gated prompting on Solana devnet.
2. Run inference locally on host device (Steve Chat-derived runtime).
3. Return responses reliably with clear payment-to-inference linkage.

## 4. Non-Goals (MVP)
- Mainnet launch
- Enterprise key management
- Complex multi-tenant scheduling
- Guaranteed operator-blind compute (beyond zero-retention policy)

## 5. Personas
- **Prompt Buyer**: wants private prompt processing, pays per request.
- **Host Operator**: runs local model on phone/device and earns micro-fees.
- **Hackathon Judge**: needs a clear demo narrative and proof trail.

## 6. User Stories
- As a buyer, I can connect wallet and see prompt price.
- As a buyer, I can pay and submit prompt in one flow.
- As a buyer, I receive response and tx proof.
- As a host, I can start/stop inference service quickly.

## 7. MVP Features
- Wallet connect + devnet payment flow.
- Payment verifier service (RPC-backed).
- Inference endpoint gated by payment proof.
- Web UI showing status: unpaid/pending/paid/processing/completed.
- Local record log (non-sensitive metadata only).

## 8. Success Metrics
- >= 3 successful paid prompts in live demo.
- Median prompt roundtrip under 45s (model dependent).
- Zero prompt persistence to disk in normal mode.

## 9. Risks
- Device uptime and thermal limits.
- RPC instability or rate limits.
- Long model latency for larger prompts.

## 10. Demo Narrative
1. User opens web app and sees price.
2. User pays on devnet.
3. Service verifies tx.
4. Prompt executes on local device model.
5. Response + transaction reference shown.
