# Current stage

[English](current-stage.md) | [Русский](current-stage.ru.md)

As of **2026-10-18**, the core campaign/FSM, control, navigation, and tracker layers are implemented. Integration and offline checks are ongoing. Fleet work is experimental. The source is an active working copy, not a frozen release.

## Checks so far

The history includes both passing and failing runs. A past pass applies to the revision and conditions checked, not automatically to the current code. A past failure cannot be assumed to persist without checking it again.

There is no tracked CI validation gate to cite. This does not mean that no local or external checks have occurred. The current full gate remains unverified.

## What remains unproven

- **Full autonomous campaign completion.** The implemented components do not yet establish a complete end-to-end run.
- **End-to-end checkpoint recovery.** Persisting state, deciding how to recover, and safely resuming still need verification together.
- **Remote VM wiring and fleet acceptance.** Complete, reliable remote integration has not been established; fleet acceptance is pending.
- **Fleet capacity.** Supported concurrency, throughput, and operating limits are not established.

## Open problems

- **RPC/shell trust.** The internal command interface cannot be trusted just because it is internal. It needs a reviewed trust model, constrained command authority, and rejection and failure cases.
- **Recorder exports.** Truncation is not redaction: shortening a recording can leave sensitive content intact. Redaction and export rules need separate review.
- **Remote adapter and tracker gaps.** Their contracts need to define availability, observation freshness, errors, and state consistency. Missing or conflicting observations can mislead coordination.
- **Rotation semantics.** Assignment, ownership, handover, interruption, and stopping need precise rules and bounded tests.
- **Sensitive artifacts and asset rights.** Each artifact needs an origin and redistribution-rights check. Unreviewed material stays out.

The [proposed demos](what-will-be-shown.md) describe how some of these questions could be explored with synthetic examples. For the project overview, see the [README](../README.md).
