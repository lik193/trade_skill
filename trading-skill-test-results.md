# Five trading skills under test

The clearest misses were a designer that turned an hourly-data question into a year-long experiment and a critic that inferred daily bets from weekly totals. The strongest results were a correct portfolio replay, a working fill ledger, and an audit that distinguished a valid timing fix from a change of strategy.

## How the tests ran

Each skill went to a separate agent with the skill text, a synthetic user request and the raw evidence it needed. The agents did not receive the expected answers. The builder changed an isolated Python simulator. I ran a separate set of CLI cases against its output and independently recalculated the reviewer's findings. A further comparison gave the FX critique prompt to an agent that had exercised the design skill, without loading the critique skill. That is one comparison using different agent histories. It cannot establish how much the skill improves the underlying model. All results concern simulated decisions.

## Orchestrate

**Passed the portfolio and promotion decisions.** On four days an early trade made $4 and occupied the only slot. A later trade made $6. The gate rejected the early trade. The agent correctly kept the gate and calculated its $8 portfolio benefit. In a separate case, a preregistered rule called for doubling simulated size if the mean increment exceeded $3 over four independent sessions. The observed increments were $5, $4, $4 and $3. It advanced to two units at $10 of stress loss against a $12 budget. It resisted a request for extra sign-offs.

**Where it was less decisive.** An options-scalping case had eight development days, 48 variants, passive orders and a log of completed round trips. The agent correctly selected an order-attempt table and requested unfilled entries. It also calculated the break-even mix of news and ordinary trades conditional on a constant $2 gross return and the quoted execution costs. The 21.9%–44.4% range is arithmetically sound under those assumptions. Its decision value is limited because the passive orders that actually fill can have different gross returns. The recommendation to revise after nonpositive attempt-level P&L also leaves an ambiguity. Those data can expose a fill-accounting problem, while one noisy development block gives weak grounds for retuning the signal.

**Change worth testing.** Ask which result would justify repairing the measurement, which would justify changing the strategy, and whether the sample can distinguish them. Skip numerical precision that cannot change the next action.

An additional prioritization check tested whether “cheapest” crowds out opportunity cost. Given one experiment slot, the agent chose the $1 experiment for rejections per dollar and the $4 experiment for expected net utility. It correctly calculated 0.50 versus 0.20 expected rejections per dollar and $0 versus $16 expected net utility. It changed its recommendation when the manager's objective changed.

## Design

**Passed identification and execution timing.** All 12 pilot buybacks involved high-short-interest stocks, and the researcher chose that flag after seeing winners. The agent recognized the missing comparison group and the limits of attributing trades to short covering. In FX, the direction of a 16:00 move became known after the snapshot. It designed a trade against that move from 17:00 to 18:00 using bid and ask. That is an executable decision schedule and a genuinely new prediction. It correctly labeled the historical quotes as fill estimates.

**Where it exceeded the evidence.** It told the buyback researcher to freeze an “original surprise-buyback rule.” The user supplied a category and releases, with no reproducible rule for deciding which releases counted as surprises. Even a pre-announcement short-interest field would only test whether high short interest predicts a different reaction. It would leave room for the announcement itself to convey different information in those stocks. In FX, the agent prescribed the next 12 monthly observations without first asking whether untouched months existed in the supplied history. It also prescribed dropping the idea if either of two sample means was nonpositive, with scant attention to uncertainty on the negative side.

**Change worth testing.** State the smallest claim the available fields actually identify. Define any label needed to select events. Use untouched existing evidence when available, and allow an inconclusive outcome on either side of zero.

## Build

**Passed all 12 external CLI cases.** The input was a stream of cumulative order snapshots. A buy of two shares at $100, updated to five shares at a cumulative average of $103 and repeated, followed by a five-share sale at $104, must end flat with $5. Summing snapshot quantities would invent fills. The implementation kept the highest sequence per order and reconciled the cash. The independent cases covered an empty stream, the example trade, full replay, a blank-price zero-quantity acknowledgment, a later price correction followed by a stale message, crossing into a short position, and all six arrival orders for a three-message fixture.

**Observed boundary.** Two conflicting five-share snapshots with the same order ID and sequence, priced at $100 and $101, produced cash of −$500 or −$505 depending on arrival order. The builder explicitly assumed identical payloads for duplicates. The contradictory input falls outside that assumption. The result exposes a gap between documenting a feed assumption and detecting a breach that changes cash. The valid-input tests establish final cash and position only. An order router with intermediate risk decisions would need a different test.

**Change worth testing.** When an asserted identity or replay guarantee affects money, exercise one contradiction. Where the feed contract leaves that contradiction unresolved, surface it to the caller before treating the resulting balance as settled.

## Review

**Passed both audits.** Four daily event returns were +$3, +$9, −$5 and −$1. The 09:59 first scores had signs +, −, +, −. Final 18:00 scores had signs +, +, −, −. The reported code bought at 10:00 using the later scores. The agent reproduced +$12, calculated the intended first-score result of −$2, and calculated +$4 for trading the prior session's final score. It explained why that last figure answers a different question. In a second case, a top-ranked strategy earned $18 among three surviving tickers. The reviewer gave a concrete counterexample to the claimed $18 lower bound when omitted historical tickers could displace the winners.

**Passed a missing-provenance follow-up.** A clean-looking historical cache selected +$4 and +$3 days and skipped a −$10 day. The only receipt showed a later bulk download. The reviewer reproduced +$7, identified the missing pre-open publication evidence, and correctly declined to claim that revisions had actually occurred. With unknown selections and fixed prices, it gave the tight range of −$10 to +$7 and named the record that would settle the issue.

**Remaining limit.** No material error surfaced across these three cases. The fixtures were small enough for exhaustive inspection, and the reviewer already had timing audits in its conversation when it saw the cache. Its ability to find an influential defect among many tables and transformations in an unfamiliar production-sized repository is unmeasured. I would keep this skill as written on present evidence.

## Critique

**Passed the portfolio mandate.** In three equally likely states, the book returned +10, +10, −30. A hedge added −3, −3, +12. Keeping it reduced the chance of losing more than 20 from one-third to zero and raised mean P&L from −10/3 to −4/3. The agent respected the stipulated loss objective and recognized that neither available choice had a positive mean.

**Failed to respect the resolution of the data.** An AI times extra exposure daily. Its four weekly returns were +2, −2, +4, −4 against a base rule's +1, −1, +4, −4. The first two weeks shared one shock. The agent correctly found zero incremental P&L and proposed randomly assigning the same extra exposure across comparable opportunities. It then asserted the last two weeks used ordinary size. Weekly equality cannot establish that. Two doubled daily bets returning +1 and −1 can cancel inside a week. It also advised keeping the comparator in production although the user had supplied no deployment status.

**Comparison.** The agent answering without the critique skill reached the same verdict, recommended a similar matched-exposure comparison, and likewise read too much into weekly equality. The dedicated skill showed no clear advantage on this example.

**Change worth testing.** Before explaining *why* aggregate P&L matched, name a different underlying sequence that produces the same totals. If the verdict depends on which sequence occurred, request the decision-level positions. Keep recommendations within the operating environment the user established.

## Revision priorities

First sharpen the designer's use of existing evidence and the critic's handling of aggregation. Preserve the orchestrator's willingness to promote a passing experiment. Add a builder check only where an ambiguous input can change the balance. The review cases give no reason to add more instructions. These results describe the original drafts, before the revisions packaged in Trading Lab 0.1.0.
