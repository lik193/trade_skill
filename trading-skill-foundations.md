# What trading judgment should change in a system

A trader sees a surprise, forms a view about who needs to act, and chooses a price at which taking the other side makes sense. The part worth teaching is how to recognize the situation, express the view as a payoff, and learn whether the judgment earned its keep. Kahneman and Klein identify learnable regularities and feedback as conditions for skilled intuition. Markets sometimes offer that combination for narrow tasks. In Taiwanese day-trader data, Barber and colleagues found persistent differences in ability, although fewer than 1% predictably earned positive abnormal returns after fees. Selecting a successful trader after the fact is a poor way to decide which habits to copy. [Kahneman and Klein](https://pubmed.ncbi.nlm.nih.gov/19739881/) · [Barber et al.](https://faculty.haas.berkeley.edu/odean/papers/day%20traders/The%20Cross-Section%20of%20Speculator%20Skill.pdf)

## Three instincts to cultivate

**Notice a detail that could prove the story wrong.** Researchers studying overnight S&P 500 futures returns proposed that market makers could unload inventory when overseas traders arrived. Japan keeps the same clock year-round. From New York, the Tokyo open moves by an hour when US daylight saving time changes. Return predictability around the open moved with it. A system designer could have spent weeks tuning an hour-of-day feature. The shift in clocks gave the researchers a way to distinguish explanations. [Boyarchenko, Larsen and Whelan](https://libertystreeteconomics.newyorkfed.org/2021/05/the-overnight-drift-in-us-equity-returns/)

**Ask how much of the idea is still available at our price.** FX researchers found that the unexpected component of a macro release moved dollar exchange rates. A bot reading that release has to find a remaining move after the first quote it can reach. An options buyer faces a different hurdle. A $100-strike straddle bought for $6 and held to expiry with the stock at $104 loses $2 per share before costs. An earlier exit requires a resale price. For an equity swing signal calculated from the official close, split the overnight gap from the following session's return and credit only the portion the position could own. Swing describes the holding horizon and applies across instruments. [Andersen et al.](https://www.aeaweb.org/articles?id=10.1257/000282803321455151) · [Options Industry Council](https://www.optionseducation.org/strategies/all-strategies/long-straddle) · [Nasdaq auction mechanics](https://www.nasdaqtrader.com/trader.aspx?id=openclose)

**Identify the risk you might be paid to own.** Someone seeking immediacy or insurance may willingly pay a premium. Ask whether the strategy can carry that exposure through the bad state, what it would lose alongside existing positions, and whether the price compensates it. A low trade count can conceal a common dollar exposure across several FX pairs. A high win rate can conceal an expensive short-volatility loss. Conversely, several defensive filters may all veto the same profitable opportunity. A retail FX study found traders increased size following winning weeks even though past performance failed to predict success in that sample. Compare any conviction-based sizing rule with fixed size on identical trades. [Ben-David, Birru and Prokopenya](https://www.nber.org/papers/w22146)

## Where to spend the next hour of development

These are hypotheses to investigate in a codebase. Each can be checked with a small piece of evidence.

| When the system does this | Investigate this first |
|---|---|
| Adds another analyst or confidence threshold | Identify the orders whose direction, timing or size would change. Shadow those decisions and compare net dollars and downside. Agreement between agents reading the same evidence adds little independent information. |
| Tunes entries against a single equity curve | Keep the entries and substitute a timed exit. Then keep the trades and use constant size. Find out which decision actually earns money. |
| Adds filters whenever a loss looks bad in hindsight | Replay the whole book with one discretionary veto removed, including missed winners, avoided losses, turnover and overlapping exposure. Judge a mandated limit against its stated purpose. |
| Calls a profitable backtest evidence of stock selection | Compare with a simple portfolio carrying similar market and sector exposure. Preserve failed variants and untouched chronological evidence. If an LLM supplied historical trade calls, its training may include that history. A preprint on ten LLMs trading CSI 300 stocks found market and style exposures explained much of the return in its masked evaluation. [Zhu et al.](https://arxiv.org/abs/2605.28359) |
| Builds infrastructure to resolve an economic uncertainty | Calculate the break-even spread, delay or event move first. If plausible execution costs wipe out the payoff, better infrastructure needs a specific way to recover the difference. |

## Five independent decisions

| Role | A finished piece of work |
|---|---|
| [Orchestrate](plugins/trading-lab/skills/trading-orchestrate/SKILL.md) | Choose and perform the cheapest observation that changes what happens next. |
| [Design](plugins/trading-lab/skills/trading-design/SKILL.md) | Give a market explanation, a tradable expression and a prediction its strongest rival would get wrong. |
| [Build](plugins/trading-lab/skills/trading-build/SKILL.md) | Deliver the smallest working implementation and reconcile a trade from decision to net cash. |
| [Review](plugins/trading-lab/skills/trading-review/SKILL.md) | Trace whether the claimed result was achievable with the data, timing, fills and capital available. |
| [Critique](plugins/trading-lab/skills/trading-critique/SKILL.md) | Grant implementation correctness and judge whether the return pays for its exposure relative to a simpler alternative. |

The Karpathy design choice is to give each skill one decision it owns and an observable finish. Start with whichever decision is unresolved. Keep any component that improves a decision enough to matter, including a simple filter or a deliberate increase in simulated risk.

## Using Trading Lab

In a Codex project with the plugin enabled, ordinary requests such as “audit this backtest” or “implement the new fill rule” can select the corresponding skill directly. To explicitly hand over the choice for an open-ended task, use `$trading-lab:trading-orchestrate`. For example, “My options simulator barely trades. Find where exposure disappears, test the most consequential veto, and implement a change if the evidence warrants it.”

To install from this workspace on another local Codex setup, run these commands from the directory containing this document.

```sh
codex plugin marketplace add .
codex plugin add trading-lab@trading-research-local
```
