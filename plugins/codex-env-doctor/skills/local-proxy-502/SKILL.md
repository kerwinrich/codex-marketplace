---
name: local-proxy-502
description: Diagnose 502/422 or "upstream connection failed" errors when Codex is routed through a local model proxy such as a CC Switch style router on 127.0.0.1. Use when requests fail with unexpected status 502 Bad Gateway or provider forwarding errors.
---

# Local proxy 502 / forwarding failure

1. Find the configured endpoint without dumping secrets: `grep -n -A6 '\[model_providers' ~/.codex/config.toml`. Note the port (for example 15722).
2. Check the port is listening: `lsof -nP -iTCP:<port> -sTCP:LISTEN`. No listener means the router app is not running — start it and retry; no config change is needed.
3. Probe the proxy: `curl -s -o /dev/null -w '%{http_code}\n' -m 10 http://127.0.0.1:<port>/v1/models`. If the route requires POST, send a minimal request instead of guessing.
4. Interpret: proxy answers but upstream fails → fault is upstream credentials/quota/network at the router, not Codex. Port closed → router process. 4xx on every call → router configuration or model name mismatch.
5. Report the exact status codes and which layer failed (Codex → router → upstream). Do not "fix" networking problems by editing `config.toml`.
