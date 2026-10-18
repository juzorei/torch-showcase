# Public-content allowlist

**Snapshot — 2026-10-18. This is a local review policy, not publication authorization.**

The source remains private. This package is not published. The word "public" in this filename identifies an intended review boundary, not a current distribution status.

## Allowed in this package

Only these five text documents are in scope:

- `README.md`
- `docs/current-stage.md`
- `docs/what-will-be-shown.md`
- `PUBLIC_ALLOWLIST.md`
- `PUBLIC_DENYLIST.md`

Permitted content is limited to:

- A coming-later description of evidence-driven automation, fault-tolerant control, navigation planning, and offline replay as future demonstration goals.
- Abstract descriptions of campaign/FSM, control plane, navigation, tracker, and experimental fleet layers.
- Honest status statements: core layers implemented; integration and offline validation ongoing; full autonomy and remote fleet acceptance pending; active working copy and feature work; not a frozen release; historical green and failure runs; no tracked CI; current full gate not established.
- Explicit limits on what is unproven, including autonomous campaign completion, checkpoint recovery, remote VM wiring, and fleet capacity.
- High-level blocker descriptions that disclose no exploitable details or operational values.
- Prose descriptions of planned synthetic demonstrations and their evidence boundaries.
- Privacy, provenance, licensing, and publication-review requirements.
- Relative links between these five documents.

## Candidate future material, not included or approved now

Original toy state diagrams, invented graphs, fabricated event timelines, and abstract worker simulations may be considered later. They must be authored independently of private artifacts, clearly labeled synthetic, and reviewed for provenance and sensitive content.

This is not permission to add files, create a runnable demo, export private data, or publish anything. No source license or redistribution permission is granted by this package.

## Review rules

1. Default to exclusion for anything not explicitly allowed.
2. Apply the denylist even to content that appears to fit an allowed category; the denylist wins in a conflict.
3. Do not copy private code, documentation excerpts, logs, sessions, recordings, or runtime assets into this package.
4. Do not treat truncation, renaming, or partial masking as sufficient redaction.
5. Separate historical observations, present unknowns, and future goals in every claim.
6. Require a separate, explicit owner decision before any publication, followed by content and rights review.

The source remains private, and the package remains unpublished.
