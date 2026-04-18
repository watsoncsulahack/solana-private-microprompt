# Software Requirements Document (SRD)

## 1. Architecture Components
1. **Web Client**: wallet UI, prompt form, result display.
2. **Payment Gateway Service**: receives tx signature, validates payment via RPC.
3. **Inference Orchestrator**: checks payment entitlement and forwards to local runtime.
4. **Local LLM Runtime**: Steve Chat-derived local model endpoint.
5. **State Store (MVP)**: local lightweight store for request metadata.

## 2. Functional Requirements
- FR1: System must require payment proof before inference.
- FR2: System must validate payment recipient, token/SOL amount, and freshness window.
- FR3: System must map one verified payment to one prompt entitlement.
- FR4: System must process prompt via local runtime and return response.
- FR5: System must expose start/stop controls for host runtime.
- FR6: System must not persist prompt/response bodies when zero-retention mode is enabled.

## 3. Non-Functional Requirements
- NFR1: Availability limited to host uptime, with health endpoint.
- NFR2: End-to-end encryption in transit (HTTPS/TLS).
- NFR3: P95 API latency target: < 2s (excluding inference).
- NFR4: Minimal dependency footprint for mobile-host feasibility.

## 4. API Draft (MVP)
- `POST /quote` -> returns price + payment instructions.
- `POST /verify-payment` -> accepts tx signature, returns entitlement token.
- `POST /infer` -> requires entitlement token + prompt.
- `GET /status/{requestId}` -> processing state and timestamps.
- `GET /health` -> component health summary.

## 5. Security Controls (MVP)
- Signed short-lived entitlement token.
- Idempotent payment verification.
- Basic rate limiting per wallet + IP.
- Optional encrypted payload mode for prompt body in transit.

## 6. Deployment Constraints
- Runs from mobile host with optional cloud relay for API ingress.
- Solana devnet RPC provider configurable.
- Local model endpoint configurable (Steve Chat runtime path).

## 7. Test Requirements
- Unit tests: payment verifier logic, entitlement checks.
- Integration tests: paid prompt success/failure paths.
- Demo tests: wallet pay -> verify -> infer -> response in one session.
