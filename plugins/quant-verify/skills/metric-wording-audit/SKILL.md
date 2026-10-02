---
name: metric-wording-audit
description: Check that user-facing labels, thresholds, and conclusions match what the code actually computes, and rewrite misleading terms in plain Chinese. Use when a metric name is ambiguous, when users misread a panel, or before shipping a dashboard.
---

# Metric wording audit

1. Pick each user-visible label or status word and locate its single source of truth in code (function + line).
2. Write three lines per label: what the code computes; what a reader assumes it means; the gap between them.
3. Any gap is a defect. Prefer renaming the label to the mechanism (for example `容量合格` instead of `可交易`) over adding a footnote, and keep one meaning per word across list and detail views.
4. Thresholds must be stated with values and windows (for example `liq_pct >= 0.30`, trailing 250 days), not "根据明确的数据规则".
5. Correlations with `n < 40` are not shown; `|r| < 0.3` is labelled 弱相关. Never show a score without its component breakdown.
6. Rewrite conclusions in plain Chinese: 不写"市场广度 0.42"，写"上涨的股票占 42%"；不写"成交额 8200 亿"，写"成交比昨天同期多两成"。数据缺失用 `—`，绝不用 0。
7. Finish with the changed strings and the exact files touched.
