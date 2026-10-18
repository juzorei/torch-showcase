# Demonstrations: existing tools and public proposals

[English](what-will-be-shown.md) | [Русский](what-will-be-shown.ru.md)

Torch already has private map and replay tools, along with a live navigation view, control panel, tracker, tracker fleet, and fleet-control UI. They are part of the assessed implementation, not hypothetical mockups. This repository publishes descriptions of them, **not their runtime, screenshots, recordings, inputs, or outputs**.

As of **2026-10-18**, **public synthetic demonstrations have not been created**. The proposals below would be new, independently authored examples using invented data. Existing private tools do not become approved public demos by shortening a recording, replacing names, or exporting a smaller map.

## What the existing private tools make inspectable

| Surface | What it exposes |
| --- | --- |
| Live map and navigation tools | Mesh, route, goal, player, deviation, remaining distance, replans, publication owner, and freshness/status distinctions. |
| Control panel | Owned-session state, command acknowledgements, timeline, errors, and pause/resume/stop handling. |
| Tracker and replay | Inventory context, loot events, run boundaries, costs, totals, diagnostics, and reconstruction of event sequences. |
| Tracker fleet | Live/quiet/down states, last-known data, polling freshness, and live-only aggregation. |
| Fleet control | Per-slot and bulk operations, resource governance, rotation, and worker state. |
| Recorder and distiller | Investigation of timelines, routes, quest observations, and combat profiles from private observations. |

These surfaces help explain decisions and investigate failures. Their existence is not evidence of full autonomous campaign completion, reliable remote deployment, profit, or capacity. The [feature catalog](features.md) gives each surface's implementation boundaries.

## Public synthetic examples worth building separately

### Hybrid decisions and action ownership

An invented observation stream could alternate between a quest task, a dialog, a fight, missing HP, and a death indication. The example would show which decision source has priority, why an empty fresh task list is not replaced by old history, and who owns input during a rate-limited hunter tick. A timeout and an exhausted plan would remain distinct from confirmed success.

### Route planning, following, and publication

Original toy polygons could demonstrate portals, disconnected components, floor selection, funnel smoothing, and an unreachable goal. A fabricated follower trace could illustrate remaining-path progress, sampled XY visibility, a combat-suspended stall window, and separate snapping/traversal bans. The view could show stale, other-map, no-player, arrived, and stalled states. This would not validate real geometry, every transport link, or exact 3D collision handling.

### Control failures and release-first transitions

Fabricated commands could receive delayed, missing, or failed acknowledgements. The model would distinguish retryable reads/releases from non-idempotent clicks and show ownership checks during pause, resume, and stop. It would model continuation of a running session, **not persisted checkpoint restore**, which the implementation does not have. A future persistence experiment would need its own scope and must be labeled as new work.

### Progression reports without pretending to act

Invented items could drive a plan-only equipment report explaining weights, confidence, defense floors, and a decision not to replace an item. A separate toy timeline could show partial bag snapshots and talent-observation generations. The example must keep a solver, an observation handshake, and an actual equipment/talent action distinct; a standalone capability table is not a universal runtime gate.

### Event tracking and observation freshness

A fabricated inventory and loot stream could contain snapshots, deltas, duplicate events, missing pages, identity changes, hub activity, and a new run. The tracker example would show attribution and uncertainty, not market-profit valuation. An aggregate view could contrast live, quiet, down, and last-known sources, with only live data included in current totals.

### Experimental worker rotation

Abstract workers could explore resource hysteresis, fairness, cooldowns, and exhausted-work handling before pause. Failure cases would include stale observations and mismatched ownership. A bounded simulation would explain scheduling semantics without claiming remote VM readiness or supporting a particular fleet size.

## What a public example would need

Each example should state its question, how its inputs were invented, the expected invariant, a failure case, and its stopping conditions. Results would apply only to that model. Historical navigation benchmarks and private replay results must not be repackaged as fresh public measurements.

Any addition requires separate owner approval and review of content, privacy, security, provenance, and rights. Use original toy geometry and fabricated events, not private source, extracted assets, real maps, or session derivatives. Imported build references need their own rights review. The current [allowlist](../PUBLIC_ALLOWLIST.md) authorizes documentation only; the [denylist](../PUBLIC_DENYLIST.md) remains the publication boundary.

Read the [architecture](architecture.md), [current stage](current-stage.md), or [project overview](../README.md) for what is implemented today.
