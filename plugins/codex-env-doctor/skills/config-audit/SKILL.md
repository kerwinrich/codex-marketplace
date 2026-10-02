---
name: config-audit
description: Audit the structure of ~/.codex/config.toml and its backups without printing secrets. Use when Codex behaves unexpectedly, provider/model routing changed, or before and after editing configuration.
---

# Config audit

1. List backups and timestamps: `ls -la ~/.codex/config.toml*`. Note `*.guard-backup-*` and `*.backup-*` files; the newest one is the diff baseline.
2. Print structure only, never whole values:
   `grep -nE '^\[|^model|^model_provider|^notify' ~/.codex/config.toml`
   Skip any line whose value looks like a credential (`bearer`, `token`, `key`, `secret`).
3. Confirm plugin/marketplace sections are intact: `grep -n -A4 '\[marketplaces\.'` and `grep -n -A2 '\[plugins\.'`.
4. Report: active provider and model, whether marketplaces/plugins are configured, whether a custom provider routes through a local proxy (base_url on 127.0.0.1), and whether backups exist.
5. Before any edit: `cp ~/.codex/config.toml ~/.codex/config.toml.bak-$(date +%Y%m%d-%H%M%S)`. Keep the change minimal, then verify with `codex plugin list` and one short `codex exec` run instead of assuming success.
