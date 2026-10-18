# Public-content denylist

**Snapshot — 2026-10-18. Default deny. The source remains private. This package is not published.**

This policy describes prohibited categories without including examples of their actual contents. It overrides the allowlist whenever there is uncertainty or conflict.

## Never include in this package

### Secrets and identity

- Secrets or their values, credentials, authentication material, session cookies, tokens, private keys, or environment exports.
- Account identifiers, personal data, device identifiers, or infrastructure identifiers derived from private operation.
- Partially masked values that could still identify or enable access to a private system.

### Private implementation and integration details

- Source code, binaries, dependencies, executable snippets, launchers, or runnable configuration.
- Memory offsets, signatures, pointer chains, memory dumps, or reverse-engineering notes.
- Exact endpoints, addresses, ports, process names, command payloads, or connection details.
- Operational instructions for accounts, proxies, remote desktop, VMs, remote adapters, or private infrastructure.
- Instructions for invoking internal RPC or shell facilities, or reproducing the untrusted command boundary.

### Private evidence and assets

- Raw sessions, logs, recordings, telemetry exports, screenshots, crash dumps, or captured network traffic.
- Real maps, meshes, routes, geometry, navigation captures, or derived copies of private world data.
- Sensitive artifacts copied from the source tree, local working directories, or runtime storage.
- Truncated recordings presented as redacted evidence. Truncation is not redaction.
- Private material relabeled "synthetic" after renaming, filtering, shortening, or cosmetic transformation.

### Unreviewed rights and provenance

- Third-party or extracted assets without established redistribution rights.
- Material with unknown origin, unclear licensing, or provenance that cannot be explained safely.
- Any implication that this package grants a license to the private source or its dependencies and assets.

### Unsupported claims

- Production readiness, deployment readiness, guaranteed reliability, or supported operating capacity.
- Proven full autonomous campaign completion or end-to-end checkpoint recovery.
- Complete remote VM wiring, validated fleet capacity, or settled fleet rotation behavior.
- A current full-gate pass inferred from historical green runs.
- Tracked CI coverage or a frozen release where neither is established.
- A claim that planned synthetic demos already exist, have passed, or validate live-system behavior.

Negative statements that explicitly identify these claims as unproven are allowed; affirmative readiness claims are not.

## Prohibited actions within this task

- Modifying the private source project.
- Running its bot, servers, diagnostic tools, tests, or live game.
- Adding any executable or runnable showcase material.
- Publishing, uploading, pushing, sharing externally, or creating a public release or repository.

## When in doubt

Leave the material out. Describe the limitation at a high level rather than inserting a realistic example. Any future inclusion needs its own authorization and privacy, security, licensing, and provenance review.

The source remains private. This five-document package is local, non-runnable, and not published.
