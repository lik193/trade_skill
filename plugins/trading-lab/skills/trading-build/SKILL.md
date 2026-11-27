---
name: trading-build
description: Build, fix, or refine trading-system code. Implement a specified rule, backtest, execution path, or accounting change and verify its behavior.
---

# Build a trading experiment

Identify the requested behavior and the trading decision or cash flow it affects. Use the project's normal entry point when one exists. Implement only the path needed to verify the change. For a new simulator, one observation through decision, executable order, position and net P&L is a useful first slice.

Keep event time, data availability and earliest eligible fill distinct. Apply executable price, units and costs once. Use the contract multiplier and lifecycle for options, currency conversion and financing for FX, or tradable prices and corporate actions for equities as relevant. If the needed quote or intrabar sequence is missing, quantify a bound or expose the assumption.

For an order-routing change, use the existing order identity and reconcile broker state after ambiguous acknowledgments before retrying. If replay assumes identical messages for one order ID and sequence, try a contradictory pair. Surface unresolved cash or position differences according to the feed contract. For simulator work, exercise the simulator directly.

Run the changed behavior through its normal interface. Trace one representative trade by hand from timestamp and size through cash flows to ending position and net P&L. Check a boundary case that could change the economic conclusion, such as a gap through a stop. Report the command, the observed reconciliation, and the material assumption left in the result. Add infrastructure only when a specific required behavior depends on it.
