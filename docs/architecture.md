# Architecture: a hybrid execution loop

[English](architecture.md) | [Русский](architecture.ru.md)

Torch is not a single visual macro, nor a memory-only planner. Its current campaign path combines state snapshots, a vision finite-state machine, quest goals, polygon navigation, combat arbitration, and an input executor. Operator controls and passive observation sit around that loop. This account follows the **2026-10-18 working-copy assessment**, including uncommitted WIP; arrows describe implemented relationships, not a verified end-to-end game run.

## 1. Observe before deciding

Two observation channels answer different questions. Memory/state snapshots provide structured game observations, while screen images help interpret dialogs, login, errors, and situations where a field such as HP is missing. Partial snapshots and read failures are explicit conditions. A fresh empty list of tasks means something different from a failed read or an old list of tasks.

DirectReader caches full state with a time-to-live, refreshes in the background, and handles reattachment. It is local to the game process. ReaderClient provides a remote-reading interface, but the campaign and hunter do not consistently use a fully remote path. Screen/input transport supports foreground and background interaction, JPEG observations, and selected image regions. Its remote reach does not remove the local-reader dependency.

## 2. Main campaign flow

The principal relationships are:

```text
Local state snapshots + screen observations
                 |
                 v
 CampaignRunner + vision state machine
       |                    |
       |              dialogs / tutorial /
       |              travel UI / recovery
       v                    |
 Fresh quest tasks          |
 + fallback knowledge      |
       |                    |
       v                    |
 Goal -> polygon route -> follower
                           |
 Combat / hunter ----------+----> shared action ownership
                                      |
                                      v
                               action executor
                                      |
                                      v
                              input/screen transport
                                      |
                                      v
                              next observations
```

This is a conceptual flow, not a literal call stack. The main entry uses CampaignRunner; hunt mode shares arbitration with route and combat work. The older recorded-point mapper is a separate path with manual next-map handling. It must not be used as a shorthand for the current runner, or described as a complete endgame controller.

The vision state machine handles login, world, combat, quest, town, and dialogs. Priority cases include network errors, announcements, and death; retry logic, a chat guard, and executor failure handling constrain action execution. Tutorial dialogs can escalate, and travel UI can select zones, chapters, and map pins. However, the `travel_map` route step is unsupported: those UI interactions do not form a general teleport planner.

Death recovery releases input before ordinary work proceeds. Checkpoint-to-town fallback can use visual evidence when HP is unavailable. This is recovery inside the game, not recovery of a persisted bot session.

## 3. Goals, plans, and evidence of progress

Quest identifiers and fresh task points inform the next goal. NPC/configuration/atlas fallbacks, observer correlation, and spawn-table knowledge supply context where direct task information is insufficient. Fresh empty tasks must not be overwritten with historical targets just to keep a plan populated.

Navigation searches polygon adjacency with A*, using exact and overlapping portals, connected components, floor selection, and slope/cliff costs. Snapping, insets, funnel smoothing, and bounded fallback produce a followable route. Virtual off-mesh, replay, and transport links extend the graph, but their existence does not verify every map connection.

The follower advances monotonically, uses bounded lookahead and sampled mesh visibility, and measures remaining-route progress. It shares the world-to-screen transform with other movement logic. Soft traversal bans do not silently become snapping bans; unreachable results are negatively cached. A resumed route continues movement state in the running process, not a saved session after restart. XY samples are an approximation, not exact 3D collision checking.

A timeout or stalled window produces a failure/progress condition, not campaign success. An exhausted plan says no planned work remains; it does not prove the game objective is complete.

## 4. One action owner at a time

Combat and hunter logic combine HP bars, nameplates, and memory data. Sticky targeting, HP-progress checks, shared bans, floor filtering, and navmesh approach guide engagement. Profile-specific rotations supply actions. Route following, combat, and hunter logic must agree on ownership before issuing movement or combat input; even a rate-limited hunter tick with no action still participates in that decision.

Combat suspends the follower's stalled-progress window, preventing a fight from being counted automatically as failed travel. Input release is part of handing off or stopping control. At the transport boundary, versions and error markers distinguish supported operations and failures. Retryable reads and releases are different from clicks: an ambiguous non-idempotent action is not blindly replayed.

Build profiles contribute level phases, pacing, and healing only where defined by the profile. In current WIP, unknown level selects the initial phase rather than disabling the entire profile.

## 5. Progression WIP is not one closed loop

Several pieces are adjacent without forming automatic character management:

| Piece | Actual relationship |
| --- | --- |
| LootLedger | Bag events are wired into the runner, with bounded pending work and partial snapshots. |
| Talent observation | Fresh-frame, generation, and close handshakes exist; runtime is observe-only, active probing disabled, no allocation. |
| Equipment solver/report | A pure solver evaluates choices; the explainable report is standalone and plan-only, not consumed by runtime. |
| Legacy tutorial equipment UI | Conditional upgrade/equip clicks remain separate; relevant templates are absent in the assessed state. |
| Capability matrix | A standalone description, not a global runtime gate covering every click. |
| Build importer | Separate reference-processing tool for skills, supports, gear, talents, and traits; not an automatic build applicator. |

These distinctions prevent a misleading diagram in which an observed item inevitably becomes equipped gear or an observed talent becomes an allocated point.

## 6. Control and observation around the loop

The controller owns an exact child process and session, using kernel locks, command identities, acknowledgements, and heartbeats. Pause, resume, and stop prioritize release of held input. There is **no persisted checkpoint restore**. Mapper and T1–T7 ownership are outside this controller's supported scope; a pure strategy module is not an endgame executor.

Navigation owners publish route/combat state atomically with a version and heartbeat. The map can distinguish stale, no-plan, other-map, no-player, arrived, and stalled states while showing mesh, route, goal, player, deviation, remaining distance, and replans.

Alongside that live map, **four UI families already exist** in the private project:

- **Control panel:** session status, command timeline, and errors.
- **Tracker:** inventory, loot, runs, totals, and diagnostics.
- **Tracker fleet:** observation freshness and aggregation across sources.
- **Fleet control:** per-slot and bulk operations, scheduling, and rotation.

These are implemented interfaces, not proposed mockups. Their existence does not mean every integration path behind them has passed live acceptance.

## 7. Passive tracking and experimental fleet

The passive event tracker separates snapshots from deltas and uses inventory-page context to interpret loot. It separates map costs, hub activity, and the next run, handles identity resets, and uses game-time durations. CSV export and event-log replay are separate capabilities; replay reads JSONL event logs, not CSV exports. The accounting does not provide complete market-profit valuation.

Tracker fleet polls concurrently against a deadline, keeps last-known values distinct from live data, and represents live/quiet/down states and poller freshness. Totals include live observations only; rendering is differential. Its loopback-bound handler remains a limitation for remote VM topology.

Fleet control adds asynchronous login, a resource governor with hysteresis, rotation fairness, cooldowns, and command-line tooling. Rotation treats exhausted work as done before pause, which is an execution-state rule rather than evidence of campaign completion. Local DirectReader dependence and remote tracker gaps keep the end-to-end fleet experimental. No supported capacity follows from the scheduler or UI.

## 8. Tools, provenance, and public boundary

Recorder and distiller tools turn private log/memory/input observations into timelines, routes, quests, and combat profiles. Health checks, template and coordinate calibration, navigation rendering and diagnostics, a knowledge API, and observer telemetry support investigation. The new ownership-aware input watchdog is standalone WIP, not a guaranteed runtime safeguard.

Some transport and mapper foundations were reused from an earlier project; this is not an all-from-scratch claim. Imported build references need rights review. Source, runtime, real map/replay demonstrations, and their inputs remain private. The public repository contains narrative documentation only; future synthetic examples would be separate work.

For details, see the [18-group catalog](features.md), [current evidence and limits](current-stage.md), [demonstration plans](what-will-be-shown.md), and [overview](../README.md).
