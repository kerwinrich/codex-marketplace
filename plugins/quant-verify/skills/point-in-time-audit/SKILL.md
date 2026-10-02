---
name: point-in-time-audit
description: Audit look-ahead bias and as_of discipline in a quant pipeline: which columns are knowable at decision time and which silently leak future data. Use when a backtest looks too good, when results change after data reloads, or before trusting a new signal.
---

# Point-in-time audit

1. Fix the decision timestamp first (`as_of`, plus intraday cutoff if any). Everything below is judged against it.
2. Inventory the inputs of the scoring path, then classify each as: knowable at `as_of` / published later / unknown.
3. Red flags to search for explicitly: same-day close or volume used for a same-day signal; revised fundamentals instead of first-release values; universe built from today's constituent list; rolling windows that include the decision bar; forward-filled fields that hide release dates.
4. For each red flag found, quote the code line and show the smallest reproduction (a symbol + date where the leaked value changes the decision).
5. Write the verdict as a table: field → knowable? → evidence → impact (none / shifts ranking / flips decision).
6. Recommend the minimal fix (shift the window, use first-release data, freeze the universe), and state what would falsify your conclusion.
