# Torch — documentation showcase

**Project snapshot — 2026-10-18:** core campaign/FSM, control, navigation, and tracker layers are implemented. Integration and offline validation are ongoing. Full autonomous campaign completion and remote fleet acceptance are pending.

**Showcase status:** curated, text-only documentation published publicly with the owner's authorization. Not runnable. No completion percentage or delivery date is claimed.

The source project remains private. This separate package describes a possible future runnable showcase; it contains no source distribution, executable demo, deployment guide, or runtime release. No runtime or demo has been published. Future additions require separate explicit authorization and content review.

## The future thesis

**Evidence-driven automation: fault-tolerant control, navigation planning, and offline replay, made inspectable through synthetic demonstrations.**

The goal is to show how an automation system can reason about progress, handle uncertainty, plan movement, and explain decisions after the fact. The eventual showcase should make failure boundaries as visible as successful behavior. This is a target for future evidence, not a claim that the private system has already met it.

## Architectural scope

The private project's high-level layers are:

| Layer | Intended role in the future story |
| --- | --- |
| Campaign / finite-state machine (FSM) | Progression, state transitions, and explicit stopping conditions. |
| Control plane | Coordination, command boundaries, and failure handling. |
| Navigation | Route planning and movement decisions. |
| Tracker | Observation, progress tracking, and evidence for inspection. |
| Experimental fleet | Exploration of multi-worker coordination and rotation semantics. |

A layer's presence does not establish end-to-end reliability or readiness for external use.

## Current stage

- The source is a working copy under active feature work, not a frozen release.
- Historical evidence includes both green and failure runs. Neither establishes the current working copy's full validation status.
- There is no tracked CI validation gate to cite for this status snapshot.
- A current full gate has not been established for this snapshot.
- Full autonomous campaign completion, checkpoint recovery, remote VM wiring, and fleet capacity remain unproven; remote fleet acceptance is pending.

Implementation of the core layers is a meaningful engineering milestone, not an end-to-end acceptance result. This status snapshot is not a release certificate.

## Why runnable demonstrations are not ready

Open blockers include the untrusted internal RPC/shell boundary; recorder truncation that is not redaction; remote adapter/tracker contract gaps; unresolved fleet rotation semantics; and sensitive-artifact, licensing, and provenance review. These must not be hidden behind polished demo material.

## What comes later

Only synthetic, offline demonstrations are proposed: a small FSM, fault-handling examples, invented navigation graphs, replay of fabricated events, and a bounded fleet simulation. None is included or claimed to pass today. Synthetic results would establish only the properties of those demonstrations, not live-system performance.

## Documents

- [Current stage and evidence limits](docs/current-stage.md)
- [Planned synthetic demonstrations](docs/what-will-be-shown.md)
- [Public-content allowlist](PUBLIC_ALLOWLIST.md)
- [Public-content denylist](PUBLIC_DENYLIST.md)

There are no installation or run instructions. The source remains private; only the curated documentation is public. Future additions require separate explicit authorization and content review.
