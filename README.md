# Trading Lab

A Codex plugin for testing trading ideas, building and refining trading systems, and checking whether results hold up after execution costs and portfolio constraints.

## Install

From the root of this repository, run:

```sh
codex plugin marketplace add .
codex plugin add trading-lab@trading-research-local
```

## Use

Describe the task in your trading project and Codex can select a matching skill. For open-ended or multi-stage work, invoke `$trading-lab:trading-orchestrate` to choose and carry out the next experiment.

| Skill | Example request |
| --- | --- |
| Design | Test whether this FX reversal survives the spread. |
| Build | Fix partial fills in the simulator and reconcile one trade. |
| Review | Reproduce this backtest and check what the strategy knew at entry. |
| Critique | Test whether a simpler exposure explains these options returns. |
| Orchestrate | Find why this strategy barely trades and test the most consequential filter. |

[Research notes](trading-skill-foundations.md) · [Synthetic test results](trading-skill-test-results.md) · [Deliberately horrible trading ideas](horrible-trading-ideas.md)
