---
name: acceptance-check
description: Run the daily acceptance check for A-share quant or data-panel projects - data freshness, point-in-time discipline, cross-sectional definitions, and label semantics. Use when the user asks to verify today's results, run the daily acceptance, or judge whether a panel or scan output is trustworthy.
---

# Daily acceptance check

Report every item as PASS / FAIL / UNKNOWN, each with the evidence (file, line, or number). Never summarise without evidence.

1. Freshness: `as_of` equals the trading day under review; universe and row counts match the previous session within expectation; missing values print as `—` + `数据暂不可用`, never `0`.
2. Point-in-time: every input behind a decision is knowable at `as_of`; no same-day close used to label a same-day signal. Name the exact column or function used for each decision.
3. Cross-sectional definitions: percentile windows default to the trailing 250 trading days; when history is shorter, print `n` and exclude the field from scoring.
4. Label semantics: for every user-visible status word (for example `可交易`), quote the defining code line and state in plain Chinese what it does and does not mean. A liquidity/capacity filter must not be presented as "can buy now".
5. Hysteresis: state changes require 2 consecutive confirmations or a 10% buffer; flag any state that flips daily.
6. Data-source reality: northbound real-time flow has not been published since 2024 - a live field claiming it is a defect. Use post-close口径 plus substitutes (两融余额, 龙虎榜, ETF 申赎, 南向资金).
7. Output closes with a 7-part conclusion card: 标题 ≤15字 → 一句话 ≤40字 → 缩略图 → 3 条带数值与时间的证据 → 接下来盯什么 → 反方声音 → 置信度 🟢/🟡/⚪.
