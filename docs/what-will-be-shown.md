# Proposed demos

[English](what-will-be-shown.md) | [Русский](what-will-be-shown.ru.md)

These are proposals for synthetic, offline examples, not demos that exist today. Inputs would be invented for each example rather than exported from private sessions.

## Examples to consider

- **Campaign / FSM.** A small progression model with successful, interrupted, and invalid transitions. Show the state changes, invariants, and conditions that stop the model.
- **Control failures.** Fabricated commands with missing, delayed, or failed responses. Show bounded retries, safe stopping, and which observations a decision relies on.
- **Navigation.** An invented graph or grid with obstacles and changing reachability. Show route selection, replanning, and an unreachable destination.
- **Replay and tracker.** A fabricated event stream with stale, duplicate, missing, and conflicting observations. Reconstruct its timeline and show where the observation contract breaks.
- **Checkpoint recovery model.** Toy states and checkpoints with interrupted transitions. Distinguish safe continuation, rejected recovery, and cases that need intervention.
- **Fleet simulation.** Abstract workers with task ownership, interruption, and handover. Explore rotation rules, assignment invariants, and failure traces within a bounded simulation.

## What an example should explain

Each example should name its question, describe how the inputs were invented, and state the expected invariant. It should include a failure case as well as a successful one, show the observations behind the result, and explain its assumptions and stopping conditions.

A result would apply to that model only. It would not establish live campaign autonomy, end-to-end checkpoint recovery, RPC/shell security, live navigation or adapter/tracker correctness, remote VM readiness, or fleet capacity.

## Before adding anything

Use original toy geometry and fabricated events, not renamed or shortened private material. Content, sensitive data, provenance, and redistribution rights need review, along with separate owner approval. The [allowlist](../PUBLIC_ALLOWLIST.md) and [denylist](../PUBLIC_DENYLIST.md) define the publication rules.

For implementation status and open problems, see [current stage](current-stage.md).
