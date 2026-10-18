# Torch

[English](README.md) | [Русский](README.ru.md)

Torch is a bot project for Torchlight Infinite built around a practical engineering problem: turning incomplete observations into coordinated game actions, then making those decisions understandable to an operator. It brings together campaign progression, combat, polygon navigation, inventory and run tracking, and controls for individual sessions and experimental groups of workers. The source remains private; this repository is its English and Russian documentation showcase.

## From observation to action

The current main path uses CampaignRunner, not just the older mapper that follows recorded points. Memory snapshots supply structured state, while a vision state machine handles screens such as dialogs, town, combat, and login. Quest identifiers and fresh task points help choose a goal, with NPC and map knowledge as fallbacks. Navigation turns that goal into a route, and a follower advances along it while checking progress.

Combat is part of this loop rather than a separate macro competing for the same controls. The hunter combines health bars, nameplates, and memory observations; targeting considers floors, reachability, and whether an enemy's health is actually changing. Route, combat, and hunter logic arbitrate action ownership, while build profiles provide level phases and rotations. Death handling takes priority and releases held input before recovery. A timeout remains a timeout, not a successful quest.

## Navigation you can inspect

The navigation layer searches connected polygons with A*, handles portals and floor selection, smooths routes, and follows them with bounded lookahead. It tracks remaining-path progress, remembers unreachable results, and separates temporary traversal bans from snapping to the mesh. Combat can suspend the stalled-movement window instead of being mistaken for a navigation failure.

An existing live map makes this work visible: mesh, route, goal, player position, deviation, remaining distance, and replans. Versioned publication and heartbeat information let the display distinguish a stale observation from arrival, a missing plan, or a stalled route. This is useful engineering feedback, although a displayed route is not evidence that every map link works.

## Operator tools and event history

Four other interface families already exist in the private project. The control panel exposes session status, command history, and errors, with owned-process pause, resume, and stop handling. The tracker presents inventory, loot, runs, totals, and diagnostics. Tracker fleet aggregates observations while separating live, quiet, unavailable, and last-known data. Fleet control adds per-slot and bulk operations, resource-aware scheduling, and rotation; its end-to-end integration remains experimental.

Recording and distillation tools support timelines, routes, quest observations, and combat profiles. Calibration, navigation diagnostics, replay, and a knowledge API help investigate why a decision was made. The project also contains a build-reference importer and an equipment decision solver. These tools have distinct responsibilities: an explainable equipment report proposes a plan, but the runtime does not consume it to equip items. Talent integration currently observes rather than allocates.

## What this snapshot means

The **2026-10-18** assessment includes uncommitted work in progress, not a frozen release. “Implemented and wired” describes a real integration path, not live acceptance. Loot-ledger events are connected to the runner; newer reports and an input watchdog remain separate work. Pause/resume exists, but persisted checkpoint restoration does not. Remote input transport also does not make the local state reader or tracker fully remote.

Full autonomous campaign completion, complete market-profit valuation, and fleet operating capacity are not established. No source tests were run for this documentation rewrite, and historical checks are not a current green result. Some transport and mapper foundations were reused from an earlier project; imported build references still require rights review.

## Explore the project

- [Feature catalog](docs/features.md) — all 18 groups, their implementation, and their boundaries.
- [Architecture](docs/architecture.md) — the actual hybrid flow and separate tools.
- [Current stage](docs/current-stage.md) — evidence, WIP, and integration questions.
- [Demonstration plans](docs/what-will-be-shown.md) — existing private map/replay tools versus public synthetic examples not yet created.

This repository contains 14 documentation files, no runnable bot, screenshots, or source exports. Publication scope is defined by the [allowlist](PUBLIC_ALLOWLIST.md) and [denylist](PUBLIC_DENYLIST.md).
