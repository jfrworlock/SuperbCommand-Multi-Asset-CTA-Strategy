# SuperbCommand Multi-Asset CTA Strategy

A systematic multi-asset trend-following research project built in Python around my **SuperbCommand** TradingView indicator, with hierarchical inverse-volatility portfolio construction and rigorous walk-forward, bootstrap, transaction-cost and holdout validation.

## Version 1.0 — Frozen Research Specification

Version 1.0 is now **frozen**. The research tested whether SuperbCommand could support a robust weekly multi-asset CTA-style allocation process across equities, rates, commodities, FX and crypto.

### Frozen V1 Architecture

- **Direction:** Long / cash
- **Frequency:** Weekly
- **Universe:** SPY, EFA, EEM, SHY, IEF, TLT, TIP, GLD, DBC, UUP and BTC-USD
- **Portfolio construction:** Hierarchical inverse-volatility weighting across asset classes and within each asset class
- **Equity Early Reversal:** 2-step 50/50 entry
- **Other Early Reversal:** Immediate entry
- **Pullbacks:** Maintain target exposure; no additional accumulation
- **Leverage:** None
- **Generic shorting:** Rejected

### V1 Research Outcome

Across the frozen **2005–2025 backtest** (1,094 weekly observations), the final strategy produced approximately:

| Metric | V1 Result |
|---|---:|
| Annualised return | 4.1% |
| Annualised volatility | 3.4% |
| **Sharpe ratio** | **1.21** |
| Sortino ratio | 1.65 |
| **Maximum drawdown** | **-6.1%** |

The architecture was frozen before opening the 2026 holdout. Transaction-cost and execution-timing stress tests were subsequently conducted without changing the strategy rules.

A central finding was that **additional complexity often failed to improve the portfolio**. Generic shorting, pullback pyramiding, dynamic strategy selection, ERC and volatility-targeting layers were therefore excluded from V1.

## Dual Trend Benchmark

A simple **Dual Trend** benchmark proved exceptionally strong and, over the common comparison sample, outperformed SuperbCommand on a risk-adjusted basis.

This became one of the most important findings of V1: a simple, robust directional trend model can be difficult to beat with a more complex state-machine approach.

Rather than discarding SuperbCommand, this result motivates the next stage of the research: testing whether SuperbCommand contains **incremental information conditional on the underlying trend regime**.

## Version 2.0 — Dual Trend + SuperbCommand

V2 will investigate a **single unified Dual Trend + SuperbCommand indicator and strategy architecture**.

The working hypothesis is:

> **Dual Trend provides the primary directional regime and baseline exposure, while SuperbCommand acts as a conditional confirmation, veto or moderation layer.**

Rather than asking SuperbCommand to determine the entire portfolio state independently, V2 will test whether its richer information can improve specific decisions made by the simpler trend model.

### Initial Research Questions

Potential V2 hypotheses include:

- Should SuperbCommand confirm or delay a Dual Trend **0% → 50%** entry?
- Can SuperbCommand distinguish genuine trend reversals from **bear-market rallies**?
- Should SuperbCommand confirm or veto a Dual Trend **100% → 50%** reduction?
- Can SuperbCommand reduce whipsaw when the fast trend signal reverses for only one or two weeks?
- Can SuperbCommand provide more intelligent **profit-taking** around weakening trends?
- Can the combined architecture support a more robust **long / short CTA framework**?
- Does SuperbCommand contain statistically and economically meaningful incremental information **conditional on Dual Trend state**?

Candidate Dual Trend horizons such as **13/52 weeks** and **12/50 weeks** may be investigated, but V2 will begin with **conditional-state attribution rather than broad parameter optimisation**.

## Research Governance

To preserve the integrity of the research process:

- **V1 remains permanently frozen.**
- 2026 is permanently treated as **seen data** for V1.
- V2 will be treated as a **new research programme**, not a retrospective modification of V1.
- New rules must demonstrate incremental value through appropriate walk-forward and robustness testing.
- Any eventual V2 specification will require a **genuinely future holdout**.
- Historical backtest results are research outputs and are not forecasts of future performance.

## Status

**V1:** Frozen  
**V2:** Design / hypothesis-generation stage
