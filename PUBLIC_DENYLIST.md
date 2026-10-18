# Public-content denylist

[English](PUBLIC_DENYLIST.md) | [Русский](PUBLIC_DENYLIST.ru.md)

The [allowlist](PUBLIC_ALLOWLIST.md) names all ten permitted files and their scope. Everything else is excluded by default. These prohibitions take priority over an allowed category, including when there is uncertainty.

## Keep out

- **Credentials and identity:** secrets, tokens, cookies, keys, environment exports, personal data, and private account, device, or infrastructure identifiers—even partially masked.
- **Code and operations:** source, executable snippets, binaries, dependencies, launchers, runnable configuration, exact endpoints, addresses, ports, process names, command payloads, and connection details. No setup or invocation instructions for accounts, proxies, remote desktop, VMs, adapters, RPC, shell, or private infrastructure.
- **Memory and game data:** offsets, signatures, pointer chains, dumps, reverse-engineering notes, real maps, meshes, routes, geometry, and derived navigation data.
- **Private history and recordings:** private documentation excerpts, development history, raw sessions, logs, telemetry, screenshots, crash dumps, network captures, and sensitive artifacts. Shortening, filtering, or renaming private material does not make it redacted or synthetic.
- **Uncleared assets:** extracted or third-party material without confirmed origin and redistribution rights. This package grants no rights to private code, dependencies, or assets.
- **Unsupported claims:** readiness, reliability, autonomy, checkpoint recovery, remote integration, fleet acceptance, capacity, or settled rotation presented as proven; a current result inferred from a historical pass or failure; CI coverage or a frozen release without evidence; proposed demos presented as existing or as proof of live behavior. Stating what is unproven is allowed.

Do not modify or run the private source, bot, servers, diagnostics, tests, or game as part of documentation work. Do not add runnable material. Future additions or publication beyond the authorized documentation require separate owner approval and content, privacy, security, provenance, and rights review.
