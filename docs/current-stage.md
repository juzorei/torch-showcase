# Current stage

**Project snapshot — 2026-10-18:** core campaign/FSM, control, navigation, and tracker layers are implemented. Integration and offline validation are ongoing. Full autonomous campaign completion and remote fleet acceptance are pending. The fleet layer remains experimental.

**Curated documentation published publicly with the owner's authorization. The source remains private. No runtime or demo has been published.** No completion percentage or release date is assigned.

## Baseline and evidence limits

The project is a working copy under active feature work, not a frozen or release-qualified snapshot. Its history includes green runs and failure runs. Historical green results are scoped to the revision and conditions that produced them; they do not transfer automatically to the current working copy. Historical failures are relevant evidence, but are not asserted to remain reproducible without a new check.

There is no tracked CI validation gate to cite. This does not establish that no local or external checks have ever occurred. It means this package cannot point to a tracked, current CI result as proof of readiness.

The current full gate is unverified. Core implementation is a milestone, while integration and offline validation remain ongoing. Full autonomous campaign completion and remote fleet acceptance still require separate evidence; neither is implied by the presence of the core layers.

## Architectural layers

| Layer | High-level scope | Evidence boundary |
| --- | --- | --- |
| Campaign / FSM | Campaign progression and state transitions. | Component presence is not proof of autonomous campaign completion. |
| Control plane | Coordination and command execution boundaries. | Fault-tolerant behavior remains a demonstration target; trust boundaries need review. |
| Navigation | Planning routes and movement. | No real-world map or end-to-end navigation guarantee is provided. |
| Tracker | Observations and progress visibility. | Visibility alone does not establish complete or consistent adapter contracts. |
| Experimental fleet | Multi-worker orchestration experiments. | Neither capacity nor safe rotation is established. |

## What is not yet proven

- **Full autonomous campaign:** no complete, independently reviewable end-to-end proof is included.
- **Checkpoint recovery:** persisted state, recovery decisions, and safe resumption have not been established as an end-to-end guarantee.
- **Remote VM wiring:** remote integration is not certified as complete or reliable; this package supplies no setup instructions.
- **Fleet capacity:** no supported concurrency, throughput, or operating envelope is claimed.
- **Current full gate:** historical results are not a substitute for a complete check of the current source state.

## Blockers

| Blocker | Why it matters | Evidence needed before a stronger claim |
| --- | --- | --- |
| Untrusted internal RPC/shell boundary | An internal interface must not be assumed trustworthy merely because it is internal. | A reviewed trust model, constrained command authority, and synthetic rejection/failure cases. No callable interface is exposed here. |
| Recorder truncation is not redaction | Shortening recorded content can leave sensitive material intact. | A separate redaction and export policy with review. Future demos should generate synthetic evidence directly rather than trim private recordings. |
| Remote adapter/tracker contract gaps | Missing or inconsistent observations can produce misleading state and coordination decisions. | Explicit contracts for availability, freshness, errors, and state consistency, illustrated with synthetic contract cases. |
| Fleet rotation semantics | Assignment, ownership, handover, and failure handling require precise definitions. | A defined rotation model with bounded synthetic cases for stale ownership, interruption, and stopping. |
| Sensitive artifacts and licensing/provenance | Private data or third-party material cannot be assumed safe or permitted to redistribute. | Artifact-by-artifact origin and rights review, with exclusion as the default. |

These are open readiness constraints, not completed remediation claims.

## Scope of this package

This is a public documentation page, not a runnable showcase. It contains editorial descriptions only. It deliberately omits operational values, integration details, private evidence, source code, and runtime assets.

A future synthetic demonstration would prove only its stated, bounded properties. It would not prove live campaign autonomy, remote deployment readiness, fleet capacity, or production reliability. The source remains private. Future additions require separate explicit approval and content review.
