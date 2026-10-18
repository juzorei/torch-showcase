# What will be shown later

**Snapshot — 2026-10-18. Curated documentation published publicly with the owner's authorization. Planned demonstrations only; no runtime or demo has been published.**

The source remains private. The proposed showcase will explain evidence-driven automation using newly authored synthetic scenarios, not exports from private sessions or live environments.

## Target synthetic demonstrations

| Target | Synthetic setup | Intended evidence | What it would not prove |
| --- | --- | --- | --- |
| Campaign / FSM | A small invented progression model with successful, interrupted, and invalid transitions. | An inspectable transition narrative, explicit invariants, and visible stop conditions. | Full autonomous campaign completion in the private system. |
| Fault-tolerant control | Fabricated commands and observations with injected missing, delayed, or failed responses. | Bounded retry decisions, safe stopping, and a clear account of what is known and unknown. | Security or reliability of a real internal RPC/shell boundary. |
| Navigation planning | An invented graph or grid with synthetic obstacles and changing reachability. | A route explanation, replanning decisions, and explicit unreachable outcomes. | Performance on real maps or meshes, or live movement reliability. |
| Offline replay and tracker | A purpose-built stream of fabricated events, including stale, duplicate, missing, and conflicting observations. | A reconstructable timeline, documented replay assumptions, and visible contract failures. | Completeness of private recordings or correctness of live adapter/tracker wiring. |
| Checkpoint recovery model | A toy state model with invented checkpoints and interrupted transitions. | A clear distinction between safe continuation, rejected recovery, and required intervention. | Proven end-to-end checkpoint recovery in the private project. |
| Experimental fleet | A bounded simulation of abstract workers with ownership, interruption, and handover cases. | Explicit rotation rules, assignment invariants, and failure traces. | Remote VM readiness, usable fleet capacity, or production scaling. |

These are design targets, not existing demo results or promises of a release date.

## Evidence standard for future material

Each proposed demo should state:

1. The narrow question it addresses and the claim it does not address.
2. How its inputs were invented, without private-data derivation.
3. The expected invariant and a counterexample or failure case.
4. The observations that support the result, including uncertainty and stopping conditions.
5. The assumptions and limits that prevent extrapolation to the private live system.

Offline replay is a future demonstration goal. No private replay data, raw sessions, or logs are bundled here. Truncating a recording does not make it redacted or suitable for distribution.

## Boundaries

- Use only invented entities, generic state names, synthetic events, and original toy geometry.
- Do not reconstruct private maps, meshes, memory layouts, operational identifiers, or integration details.
- Do not include credentials, secrets or their values, live addresses, exact endpoints or ports, or process names.
- Do not provide account, proxy, remote-desktop, or VM setup instructions.
- Do not turn a synthetic demonstration into a production or live-game claim.
- Treat licensing and provenance review as prerequisites, not assumptions.

## Release posture

This public documentation package contains only the five named Markdown documents. Demo assets, code, recordings, binaries, and deployment material are not included. The allowlist defines content boundaries, not blanket permission to publish future additions.

The source remains private. Any future demo implementation or addition is separate work requiring explicit authorization and content review.
