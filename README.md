# SuperbCommand Multi-Asset CTA Strategy

A systematic multi-asset CTA research project in Python exploring conventional trend following, my **SuperbCommand** indicator, anticipatory trend-transition modelling and machine learning.

The project is organised into independently governed research versions. Earlier specifications remain frozen rather than being retrospectively modified as later approaches are developed.

## Version 1.0 — SuperbCommand Multi-Asset CTA

V1 tested whether SuperbCommand could support a robust weekly multi-asset allocation process across equities, rates, commodities, FX and Bitcoin.

### Frozen V1 Architecture

- **Direction:** Long / cash
- **Frequency:** Weekly
- **Universe:** 11 markets / ETFs across major asset classes
- **Portfolio construction:** Hierarchical inverse-volatility weighting
- **Equity Early Reversal:** 2-step 50/50 entry
- **Other Early Reversal:** Immediate entry
- **Pullbacks:** Maintain target exposure
- **Leverage:** None
- **Generic shorting:** Rejected

### V1 Research Outcome

Across the frozen **2005–2025 backtest**:

| Metric | V1 Result |
|---|---:|
| Annualised return | 4.1% |
| Annualised volatility | 3.4% |
| **Sharpe ratio** | **1.21** |
| Sortino ratio | 1.65 |
| **Maximum drawdown** | **-6.1%** |

A major V1 finding was that additional complexity frequently failed to improve the portfolio. A simple Dual Trend benchmark was particularly difficult to beat on a risk-adjusted basis.

**Status: FROZEN**

---

## Version 2.0 — Anticipatory Trend-Transition Strategy

V2 changed the research question.

Rather than asking SuperbCommand to replace conventional trend following, V2 investigated whether **transition information can anticipate changes in established trend signals and recover part of the return sacrificed by conventional trend confirmation**.

The resulting architecture is:

> **Conventional Trend Following + Conditional Anticipatory Transition Alpha**

### V2 Research Design

V2 expanded the research universe to **53 markets** across equity indices, commodities, FX, bonds/rates and Bitcoin.

The conventional CTA sleeve uses a slow **2-of-3 trend ensemble**:

- 252-observation time-series momentum
- 100/300 moving-average trend
- 252-observation breakout/channel trend

A separate transition model estimates the probability that an apparent reversal will become a **genuine conventionally confirmed trend transition**.

The strongest early-transition information came from:

- distance to conventional trend confirmation;
- multi-horizon momentum and incumbent-trend deterioration;
- trend age and maturation geometry;
- SuperbCommand Early Reversal;
- broader SuperbCommand oscillator/state alignment;
- Adaptive SuperTrend alignment.

MACD divergence and explicit volatility features did not add sufficient independent predictive value, while HMM latent-state models were tested extensively and rejected from the production architecture.

The frozen transition classifier is a **Random Forest combining conventional transition geometry with SuperbCommand information**.

### Practical V2 Strategy

Eligible high-probability transition candidates:

1. must exceed a fully causal historical **80th-percentile probability threshold**;
2. wait **21 market observations** before anticipatory entry;
3. progressively accumulate over **42 observations**;
4. expire after **126 observations** if the successor trend is not confirmed.

Bear-to-bull transitions receive greater anticipatory exposure than bull-to-bear transitions.

The conventional and transition strategies are constructed as **independent risk sleeves** and combined:

**75% Conventional Trend / 25% Transition**

followed by final portfolio volatility targeting.

### V2 Research Outcome

Canonical expanding historical pseudo-OOS testing covers **2008–2025**.

| Metric | Conventional CTA | V2 Hybrid |
|---|---:|---:|
| Annualised return | 2.56% | **5.25%** |
| Annualised volatility | 7.69% | 10.42% |
| Sharpe ratio | 0.333 | **0.504** |
| Maximum drawdown | -16.40% | **-16.43%** |

The transition model's economic advantage was weak immediately after candidate formation but became materially stronger from approximately the **21-observation horizon**, supporting the interpretation that it identifies developing transitions rather than exact turning points.

The improvement survived probability-threshold, entry-delay, ramp, transition-allocation, asset-exclusion and subperiod stress tests. Transition alpha was strongest in **equity indices**, although the strategy remains multi-asset.

**Status: FROZEN — V2 research specification passed**

---

## Version 3.0 — ML Transition Strategy Research

V3 is the next challenger programme. It will only earn a frozen **V3.0** specification if it produces a material and robust improvement over V2.

The central question is:

> **Can machine learning improve the probability, timing, evolution and state-dependent economic payoff of trend transitions beyond the frozen V2 benchmark?**

Planned research includes:

- gradient-boosted and other supervised ML challengers to the V2 Random Forest;
- survival / hazard modelling of **time to trend confirmation**;
- Markov-switching regression for state-dependent transition payoffs;
- continuously updated transition and invalidation probabilities;
- practical DCA / partial-adjustment rules for building transition exposure;
- longer pre-2000 historical validation where reliable data are available;
- expansion toward a broader institutional multi-asset universe;
- improved futures, FX carry, total-return and transaction-cost modelling.

V2 will remain the immutable control throughout V3 research. New complexity will be retained only where it demonstrates incremental out-of-sample and economic value.

**Status: RESEARCH / CHALLENGER PROGRAMME**

---

## Research Governance

- **V1 and V2 remain permanently frozen.**
- Later versions are new research programmes, not retrospective modifications of earlier results.
- Time-series validation is chronological and causal; random train/test splitting is avoided.
- Failed hypotheses and rejected models are retained as research findings.
- Model selection considers calibration, predictive information, economic value and robustness rather than headline Sharpe alone.
- Historical pseudo-OOS results are not equivalent to a genuinely prospective holdout.
- A future holdout begins only after a specification has been frozen.
- Backtest results are research outputs and are not forecasts of future performance.

## Project Status

**V1 — SuperbCommand Multi-Asset CTA:** Frozen  
**V2 — Anticipatory Trend-Transition Strategy:** Frozen  
**V3 — ML Transition Strategy:** Research / design
