---
name: trading-review
description: Audit whether a trading system's code, data, execution assumptions and accounting support a reported backtest or observed trading result.
---

# Review a trading result

Take the reported result as a claim to reproduce. Follow the real entry point on the supplied data. Trace a consequential trade or skipped order from what the system could know, through the earliest permitted order and fill, to broker or simulated cash flows. Inspect the assumptions most capable of changing the conclusion.

For example, trace the publication time of a release, the broker's bid and ask near an FX signal, the age of both sides of an option quote, or which side of an overnight gap an equity position held. Check exposure, funding, multiplier, expiry, dividends or borrow when they enter that trade. Reconcile a portfolio total where individually plausible trades could double-spend capital.

Inspect how the reported sample was selected. Count known trials, date the last rule change, and identify reuse of validation data. If a model actually made historical decisions, check whether its training period or retrieval inputs could reveal outcomes. For deterministic rules authored by AI, inspect the rule's own inputs and development history.

Lead with findings in order of impact. Give a reproducible trade, file or data location, expected behavior and measured change to the result, or an explicit bound when rerunning is impossible. Distinguish an observed defect from missing evidence. If the claim reproduces, say exactly what you verified and under which fill assumptions.
