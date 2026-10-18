# Public-content denylist

[English](PUBLIC_DENYLIST.md) | [Русский](PUBLIC_DENYLIST.ru.md)

The [allowlist](PUBLIC_ALLOWLIST.md) authorizes exactly 14 documentation files. Everything else is excluded by default; these restrictions take priority when categories conflict or content is uncertain.

## Keep private

- **Secrets and identities:** credentials, keys, tokens, cookies, environment exports, personal data, and private account, device, or infrastructure identifiers, including partially masked values.
- **Source and runtime:** code or source excerpts, binaries, dependencies, launchers, working configurations, command payloads, exact endpoints, connection details, and instructions for operating the bot or private services. No account, proxy, remote-desktop, VM, or transport setup recipes.
- **Memory and game data:** offsets, signatures, pointer chains, dumps, memory-access recipes, reverse-engineering instructions, raw or derived real maps, meshes, routes, and geometry.
- **Sessions and artifacts:** private documentation excerpts, development-history exports, recordings, logs, telemetry, screenshots, crash dumps, network captures, and session derivatives. Truncation, renaming, filtering, or partial masking is not sufficient redaction.
- **Traceability leaks and uncleared assets:** external URLs, local machine paths, private source file/line references, revision hashes, and extracted or third-party materials without verified redistribution rights, including imported build references.
- **Unsupported claims:** implemented code presented as live acceptance; historical checks or definition counts presented as current coverage/green status; persisted checkpoint restore presented as existing; autonomy, profit, remote readiness, fleet capacity, or universal capability gating without evidence; proposed public demos presented as completed. Accurate descriptions of implemented functionality and its limits are allowed.

Documentation work must not read the private source again, modify or run the bot, tests, diagnostics, services, or game, or initiate network activity. No commit, push, runtime files, screenshots, or source exports belong to this rewrite. Further additions or publication actions require separate owner approval and review. No rights to private code or assets are granted.
