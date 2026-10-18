# Torch

[English](README.md) | [Русский](README.ru.md)

Torch is a bot project for Torchlight Infinite, with a campaign state machine, controls, navigation, and a tracker.

## Components

- **Campaign / FSM** handles progression, state transitions, and stopping conditions.
- **Controls** coordinate actions and command execution.
- **Navigation** plans routes and movement.
- **Tracker** makes observations and campaign progress visible.
- **Fleet** explores coordination and rotation across multiple workers.

## Status

As of **2026-10-18**, the core campaign/FSM, control, navigation, and tracker layers are implemented. Integration and offline checks are ongoing; the fleet layer is experimental. Full autonomous campaign completion and remote fleet acceptance are not yet proven.

The [current-stage notes](docs/current-stage.md) cover test history, open integration problems, and what still needs verification.

## What's in this repository

The source is private. This repository contains documentation in English and Russian. There is no runnable bot or demo here.

The [demo proposals](docs/what-will-be-shown.md) describe possible synthetic, offline examples of state transitions, control failures, navigation, replay, checkpoint recovery, and worker coordination—not a demonstration in the live game.

Publication rules: [allowed materials](PUBLIC_ALLOWLIST.md) · [excluded materials](PUBLIC_DENYLIST.md).
