# Current stage

[English](current-stage.md) | [Русский](current-stage.ru.md)

**Assessment date: 2026-10-18.** Torch is an active private working copy, including uncommitted WIP, not a frozen release. This page summarizes the supplied source assessment; the documentation rewrite did not re-read or execute the private source. “Implemented and wired” means a component is connected in the stated path, not that it has passed live acceptance.

## What is already substantial

The main CampaignRunner combines memory/state observations, a vision state machine, quest goals, navigation, combat, and input arbitration. Polygon planning and route following include floor handling, progress measurement, unreachable caching, and ownership-aware publication. Tutorial/dialog handling, travel UI interactions, and priority death recovery are also implemented, with the limits described in the [catalog](features.md).

The live map and four other UI families exist: control panel, tracker, tracker fleet, and fleet control. They expose navigation state, session commands and errors, inventory and run history, aggregate observation freshness, and worker operations. Recording, replay, calibration, diagnostics, and build-reference processing are real private tools, not only future demonstration ideas.

## WIP and intentionally separate paths

| Area | Current implementation | Important boundary |
| --- | --- | --- |
| LootLedger | Bag events connected to the runner; bounded pending work and partial snapshots. | This is not a complete observe–decide–equip loop. |
| Talents | Fresh-frame, generation, and close handshakes implemented. | Runtime observes only, with active probing disabled and no allocation. |
| Equipment | Pure decision solver plus a new explainable report. | Report is standalone and plan-only, not a runtime consumer. |
| Tutorial equipment | Separate conditional upgrade/equip UI clicks remain. | Relevant templates are absent; the capability matrix is not a universal click gate. |
| Builds | Profile phases, pacing, and profile-specific healing. | Unknown level currently selects the initial phase; not all actions are disabled. |
| Input watchdog | New standalone tool with ownership checks. | Not established as a general runtime safeguard or part of the general validation gate. |
| Legacy and endgame work | Recorded-point mapper and a separate pure strategy module. | Manual next-map handling remains; controller ownership of mapper/T1–T7 is unsupported. |

## Evidence and checks

No source tests were executed for this rewrite. There is no tracked CI gate establishing the current full state. The available history includes successes and failures: neither an old pass nor an old failure automatically describes today's working copy. Counts of test definitions are not execution results or coverage evidence and are not used here as a quality metric.

The new watchdog suite was omitted from the general gate. Ignored local fixtures and external harness conditions can affect checks. “Offline” checks may still use loopback communication and local files; the label does not mean every check is isolated from the environment. Historical navigation benchmarks are not fresh measurements. This documentation claims neither a current green full suite nor complete coverage.

## Known integration boundaries

- **Campaign completion:** a timeout or stall is not success, and plan exhaustion is not verified completion. Fresh empty quest tasks must not be replaced with stale history. Full autonomous end-to-end campaign completion remains unproven.
- **Travel and navigation:** travel UI exists, but the `travel_map` route step is unsupported. Configured off-mesh/replay/transport links are not validated on every map. Sampled XY visibility is not exact 3D collision checking.
- **Recovery:** release-first pause/resume/stop and in-game death recovery exist. Persisted checkpoint restore is absent, rather than merely awaiting an acceptance run.
- **Remote execution:** a remote ReaderClient and remote input transport exist, but DirectReader remains local and campaign/hunt are not fully remote. The tracker handler is loopback-bound, leaving a remote-VM topology gap.
- **Fleet:** UI, worker controls, resource hysteresis, fairness, cooldowns, and tooling are implemented. Rotation handles exhausted work as done before pause; this is not proof of a completed game objective. End-to-end fleet acceptance and supported operating capacity are not established.
- **Economics:** the tracker records loot, costs, and runs, not complete market valuation. No profit result follows from event totals.

## What further verification needs to distinguish

A meaningful integration assessment would separate observations from actions and action attempts from confirmed outcomes. It would exercise missing state, executor errors, ownership handoffs, death, combat interruption, and stalled movement; confirm freshness across navigation and tracker displays; and examine remote contracts and rotation completion ordering. An internal command channel still needs a reviewed trust boundary and failure behavior. None of these questions is answered merely by the presence of a UI or a callable component.

Private map/replay tools can support investigation, but their outputs are not public evidence here. Public synthetic examples have not been created, and even a successful future toy example would establish only its own model's behavior.

## Provenance and publication

Transport and mapper foundations include reuse from a prior project. Imported build references require origin and rights review. Recorder exports need review too: truncating, renaming, or partially masking private recordings does not make them safe synthetic data. The source, runtime, real maps, sessions, and screenshots remain private.

Read the [architecture](architecture.md) for how the pieces connect, [demonstration plans](what-will-be-shown.md) for the public/private distinction, or return to the [overview](../README.md). Publication remains bounded by the [allowlist](../PUBLIC_ALLOWLIST.md) and [denylist](../PUBLIC_DENYLIST.md).
