# codex-marketplace

A Codex plugin marketplace hosted on GitHub.

## Use it

```sh
codex plugin marketplace add kerwinrich/codex-marketplace --ref main
codex plugin list
codex plugin add hello-codex@codex-marketplace
```

## Layout

```
.agents/plugins/marketplace.json     # marketplace manifest (root)
plugins/hello-codex/
├── .codex-plugin/plugin.json        # plugin manifest
└── skills/hello-codex/SKILL.md      # skill
```

## Add a plugin

1. Copy `plugins/hello-codex` to `plugins/<your-plugin>`.
2. Update `.codex-plugin/plugin.json` (`name`, `version`, `description`).
3. Add an entry to `.agents/plugins/marketplace.json`.
4. Bump `version` in `plugin.json` so `codex plugin marketplace upgrade` picks up the change.

## Refresh after pushing

```sh
codex plugin marketplace upgrade codex-marketplace
```
