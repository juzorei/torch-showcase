# Feature catalog

[English](features.md) | [Русский](features.ru.md)

Torch combines campaign automation, navigation, combat, observation, and operator tools for Torchlight Infinite. This catalog covers **18 groups** in the source assessment dated **2026-10-18**, including uncommitted work in progress (WIP). It describes implementation, not a frozen release or live acceptance report.

**W — implemented and wired** means the relevant code has a caller in the described path. It does not mean the whole feature has passed a live run. **Standalone** means a tool or model exists separately from the main runtime. **WIP** marks unfinished integration; one group can contain all three. Boundaries below are part of each feature's description.

## 1. Memory and state snapshots

**W, with partial-data handling.** State snapshots represent available observations, missing fields, and read failures rather than assuming every read is complete. DirectReader provides a full-state cache with a time-to-live, background refresh, and reattachment handling. Consumers must still distinguish an unavailable value from a valid empty result.

**Boundary.** DirectReader reads a local process. A remote ReaderClient also exists, but its existence does not make the campaign and hunter fully remote. The public description covers contracts and freshness, not memory-access recipes.

## 2. Input and screen transport

**W.** The transport supports foreground and background input, held-key release, protocol versions, explicit error markers, and JPEG screen observations with region-of-interest support. Input and screen access form a shared execution boundary rather than independent click loops scattered through the project.

**Boundary.** Reads and release operations can be retried within their contracts. A click or another non-idempotent action must not be blindly replayed after an ambiguous response. Transport availability alone does not establish remote state-reader integration.

## 3. Campaign runner and legacy mapper

**W, distinct paths.** The main execution path uses CampaignRunner to coordinate campaign work. Hunt mode uses shared arbitration with the other action owners. The older mapper follows recorded points and relies on a manual next-map transition; it is not the description of the current campaign architecture.

**Boundary.** Keeping the legacy path available does not turn it into a complete endgame engine. A campaign runner and an exhausted action plan are not evidence of completed campaign objectives.

## 4. Vision state machine and executor

**W.** A vision-driven finite-state machine recognizes login, world, combat, quest, town, and dialog situations. Priority handling includes network errors and announcements; retry behavior, a chat guard, and executor-failure handling address cases where a proposed action cannot safely proceed.

**Boundary.** This is a hybrid system: visual state handling works alongside memory observations and route logic. A recognized screen or a dispatched action is not, by itself, proof that the intended game transition happened.

## 5. Tutorial, travel UI, and death recovery

**W, with explicit limits.** Tutorial handling escalates dialog interactions. Travel UI logic deals with zones, chapters, and map pins. Death has priority over normal activity, releases held input, and supports a checkpoint-to-town fallback; visual evidence can be used when HP data is missing.

**Boundary.** The route step named `travel_map` is unsupported. Interacting with teleport UI is not a general teleport planner. Returning from a game checkpoint is also different from restoring a saved bot session.

## 6. Combat, hunter, and action ownership

**W.** Combat combines HP bars, nameplates, and memory observations. Sticky targets, HP-progress checks, shared target bans, floor filtering, and navigation-mesh approach logic help keep pursuit tied to useful progress. Build-specific rotations supply combat actions, with release handling when control changes.

Route following, combat, and the hunter arbitrate ownership. Even an empty, rate-limited hunter tick participates in ownership decisions instead of implicitly handing movement to a competing controller.

**Boundary.** These mechanisms describe implemented coordination, not proof of reliable unattended combat across encounters.

## 7. Quest goals and progression evidence

**W.** Quest identifiers and fresh task points feed goal selection. NPC, configuration, and atlas fallbacks provide additional candidates; observer correlations and spawn-table knowledge support interpretation. A fresh empty task result must not be replaced with old task history merely because that history contains a target.

**Boundary.** Timeout and stalled progress are not success signals. Exhausting the current plan does not verify campaign completion. Goal selection needs evidence of the resulting transition, not just evidence that an action was attempted.

## 8. Polygon navigation and map connectivity

**W.** Polygon navigation uses A* over real adjacency, exact or overlapping portals, connected components, slope and cliff costs, and floor-aware selection. Snapping, inset handling, funnel smoothing, and bounded fallback shape the route. Virtual off-mesh, replay, and transport links extend connectivity where configured.

**Boundary.** Link support is not validation of every link on every map. Real maps, meshes, and derived routes remain private; the public description explains the algorithmic structure only.

## 9. Route following and recovery

**W.** The follower advances monotonically along a route, uses bounded lookahead and sampled mesh line-of-sight, and shares a world-to-screen transformation with other movement consumers. It can resume routes and measures remaining-path progress rather than only distance to the goal.

Soft traversal bans are separate from snapping rules. Unreachable results have a negative cache, and combat suspends the stalled-progress window so fighting is not automatically mistaken for failed movement.

**Boundary.** Sampled XY checks are not exact three-dimensional collision detection. Resuming a route in the running process is not persisted checkpoint restoration.

## 10. Navigation publication and live map

**W, existing UI.** Route and combat owners publish versioned navigation state atomically, with a heartbeat. The live map displays mesh, route, goal, player position, deviation, remaining distance, and replans. Its status model distinguishes stale data, no plan, another map, no player, arrived, and stalled states.

**Boundary.** A drawn line is not proof that a route was traversed. Freshness, map identity, and the publishing owner matter when interpreting the display. The UI exists privately; no screenshot or runtime is included here.

## 11. Build profiles and reference importer

**W plus separate tooling.** Build profiles define level phases, combat pacing, and profile-specific healing. Current WIP selects the initial phase when the level is unknown; it does not disable all profile actions. A separate build importer handles skills, supports, gear, talents, and traits, with awareness of incomplete reference cuts, name resolution, and snapshot differences.

**Boundary.** Importing a build reference does not mean its choices are applied automatically in the game. Imported reference material needs a provenance and redistribution-rights review before publication.

## 12. Equipment decisions and plan-only reports

**Implemented solver; standalone reporting WIP.** The pure equipment solver considers weights, deadband, confidence, defense floors, death-adaptive adjustments, dual wielding, legendary items, and cooldowns. A newer explainable report presents the reasoning and a **plan only**; the running bot does not consume that report to equip items.

**Separate legacy behavior.** Conditional tutorial upgrade/equip UI clicks remain in an older path, while the relevant templates are absent in the assessed state. The standalone capability matrix is not a global gate blocking every such click. Neither the solver nor the report establishes solved automatic equipment management.

## 13. Loot ledger and talent observation

**Hybrid WIP.** LootLedger bag events are wired into the runner with bounded pending work and partial-snapshot handling. Talent observation implements fresh-frame, generation, and close handshakes to associate observations with the correct interaction lifecycle.

**Boundary.** The runtime talent path is observe-only, with active probing disabled and no talent allocation. A standalone capability matrix describes capabilities; it does not govern every runtime action. Wired bag events, observation handshakes, and standalone reports must not be presented as one completed automatic progression loop.

## 14. Session control and control panel

**W, existing UI.** Control uses exact child-process and session ownership, kernel locks, command identities, acknowledgements, and heartbeats. Pause, resume, and stop prioritize input release before the requested transition. The control panel exposes a timeline, errors, and status rather than only start/stop buttons.

**Boundary.** Pause/resume does not restore a persisted checkpoint; that capability is absent. Mapper and T1–T7 ownership are not supported by this controller. A separate pure strategy module is not an endgame execution engine.

## 15. Passive event tracker

**W, existing UI.** The tracker separates snapshots from deltas, combines inventory-page context with loot observations, and distinguishes map costs, the next run, and hub activity. Identity resets and game-time durations keep event attribution explicit. CSV export and event-log replay are separate capabilities; replay reads JSONL event logs, not CSV exports.

Its UI contains inventory, loot, runs, totals, and diagnostic views. This is an implemented observation surface, not a proposed dashboard.

**Boundary.** Event accounting is not complete market-price valuation or proof of profit. Private event streams and replay inputs are not published.

## 16. Tracker fleet

**W, existing UI; remote gap remains.** The tracker fleet polls in parallel against a deadline, distinguishes live, quiet, and down states, retains last-known observations, and tracks poller freshness. Aggregate totals use live observations only; differential rendering updates changed information without rebuilding the whole view.

**Boundary.** Last-known data is not current data. The handler remains loopback-bound, leaving a remote-VM topology limitation. This observation aggregator is distinct from the fleet controller that schedules and controls workers.

## 17. Fleet control and rotation

**Implemented surfaces; experimental end-to-end.** Fleet has an actual UI with per-slot and bulk controls, asynchronous login handling, a resource governor with hysteresis, rotation fairness and cooldowns, and command-line tool wiring. VM infrastructure is part of the design at a high level, not a public deployment recipe.

**Boundary.** Rotation handles exhausted work as done before pause; that ordering is not verification of the in-game objective. Local DirectReader dependence and the tracker remote gap remain. Worker controls and scheduling logic do not establish fleet acceptance or a supported capacity.

## 18. Recording, diagnostics, and developer tools

**Implemented tools plus standalone WIP.** A recorder combines log, memory, and input observations; a distiller derives timelines, routes, quests, and combat profiles. Other tools cover health checks, templates, coordinate calibration, navigation diagnostics and rendering, a knowledge API, and observer telemetry. A new input watchdog is standalone WIP with ownership checks.

**Boundary.** Tool existence is not a guarantee of a corresponding product button or runtime integration. Private map and replay demonstrations already exist in the toolset; public synthetic demonstrations have not been created. Recorder outputs, memory details, and runtime artifacts stay private.

## Reading the catalog as a system

The [architecture](architecture.md) connects these groups into the actual hybrid execution flow. The [current stage](current-stage.md) separates implementation from evidence, and [demonstration plans](what-will-be-shown.md) distinguish existing private tools from future public examples. Return to the [project overview](../README.md).
