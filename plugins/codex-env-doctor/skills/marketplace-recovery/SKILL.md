---
name: marketplace-recovery
description: Recover Codex plugins or marketplaces that disappear after an app update, or when a marketplace fails to load. Use when the user says plugins vanished, a marketplace is missing, "failed to load configured marketplace snapshot", or asks whether a Codex update requires reinstalling plugins.
---

# Marketplace recovery

Durable state vs derived state (verified on Codex 26.930 / CLI 0.155):

- Durable: `~/.codex/config.toml` holds `[marketplaces.<name>]` with `source_type = "git" | "local"`, `source`, optional `ref` and `sparse_paths`, plus `[plugins."<plugin>@<marketplace>"] enabled = true`.
- Derived: Git snapshots at `~/.codex/.tmp/marketplaces/<name>`, plugin copies at `~/.codex/plugins/cache/<marketplace>/<plugin>/<version>`. Deleting them loses nothing.

Procedure:

1. Read the durable state first: `grep -n -A4 '\[marketplaces\.' ~/.codex/config.toml` and `grep -n -A2 '\[plugins\.' ~/.codex/config.toml`. If both are present, no reinstall is needed.
2. `codex plugin marketplace list` and `codex plugin list` to see which roots resolve and which plugins still report `installed, enabled`.
3. If a root is missing or errors with `marketplace root does not contain a supported manifest`, run `codex plugin marketplace upgrade [<name>]`. This re-clones and rebuilds caches; the enabled state in config survives.
4. If the clone fails (`early EOF`, `RPC failed`, `curl 28`, `Couldn't connect to server`), it is a network problem, not a Codex problem. Retry on a stable network, or clone manually and register a `local` marketplace pointing at that directory for full network independence.
5. Only after those steps consider removing/re-adding a marketplace. Never hand-edit or delete the marketplace/plugin sections as a first move.

Rules: never read or print `.env`, `auth.json`, or token values while diagnosing.
