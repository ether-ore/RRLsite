---
title: Historical assumptions reference
description: Inflation, equity, and bond returns by US market era (1872–2022) from the Robert Shiller dataset, expressed in the nominal-return convention Retirement Risk Lab uses. Six named stress-test scenarios (Long-run baseline, Stagflation, Great Depression, Lost Decade, Long bull market, Post-GFC recovery) you can drop straight into the app.
og_image: assets/macos/02_survival.png
og_image_alt: Retirement Risk Lab Survival by Age chart
---

# Historical assumptions reference

*This is also Appendix A of the [User Guide](manual.md). Same content; published here at its own URL so people searching for things like "Stagflation Monte Carlo retirement" or "Shiller dataset returns" can land directly on it.*


The Suggested settings section gave you postures organized by planning intent. This appendix gives you a different cut of the same problem: **what did each input value actually look like during specific historical regimes?** It exists so you can run an "if a Stagflation-style decade happened again, does my plan survive it?" check using inputs grounded in what actually happened, not a generic conservative posture.

The data comes from the **Robert Shiller dataset** — annual US equity and 10-year Treasury return series, with CPI, going back to 1872. The figures below are derived from that dataset's 151-year run (1872–2022).

### A.1 — Convention used here

**All return figures in this appendix are nominal**, with dividends/coupons reinvested. They match the convention the rest of the manual uses and the convention the engine expects: type the nominal mean return into **Mean annual return**, and the **Inflation rate** field separately handles how your spending grows over time. The simulator does NOT also subtract inflation from the return — doing so would double-count.

If you have an old reference that quotes real (inflation-adjusted) returns, the conversion is:

```text
nominal = (1 + real) × (1 + inflation) − 1
```

The original Historical Assumptions Guide that preceded this appendix was published with real-return figures. The conversion to nominal is mechanical given each era's inflation rate, so the tables below contain the same underlying observations re-expressed in the convention RRL uses.

### A.2 — What these numbers are and are not

**What they are:** historical observations from a single dataset covering US markets (S&P 500 and predecessor index for equities; 10-year US Treasuries for bonds). Each figure is the arithmetic mean of annual returns within the named era.

**What they are not:**

- **Not forecasts.** Past return distributions, volatility levels, correlation structures, and inflation regimes do not predict future ones.
- **Not international.** US equity and US Treasuries only; international holdings, REITs, commodities, and other asset classes are not represented.
- **Not a sequence replay.** Using these numbers in RRL produces a parametric normal Monte Carlo result — independent and identically distributed (i.i.d.) normal draws each year. That is not the same as replaying actual historical sequences. Real sequences carry serial correlation, skew, and fat tails that a normal i.i.d. model does not reproduce.

### A.3 — Inflation by era

Use these to calibrate the **Inflation rate** field. Mean is the simple average of annual CPI change within the era; SD is the sample standard deviation.

| Era | Yrs | Mean % | SD % | Lowest yr | Highest yr | Character |
|---|---|---|---|---|---|---|
| Full history (1872–2022) | 151 | 2.3 | 5.7 | -14.0 | 20.4 | Full-range baseline |
| Great Depression (1929–1939) | 11 | -1.7 | 4.8 | -10.3 | 3.0 | Deflation — prices fell |
| WWII & postwar boom (1940–1965) | 26 | 3.3 | 4.2 | -2.1 | 18.1 | Moderate, with WWII spike |
| Stagflation (1966–1982) | 17 | 6.9 | 3.4 | 3.0 | 13.3 | High and persistent |
| Long bull market (1983–1999) | 17 | 3.3 | 1.3 | 1.1 | 6.1 | Declining and tamed |
| Lost Decade (2000–2009) | 10 | 2.5 | 1.1 | 0.1 | 4.1 | Low and stable |
| Post-GFC recovery (2010–2019) | 10 | 1.8 | 0.7 | 0.7 | 3.0 | Historically low |
| Recent (2010–2022) | 13 | 2.5 | 2.0 | 0.7 | 7.0 | Low, then sudden spike |

**Note on deflation:** the Depression-era mean of -1.7% can look favorable in isolation — deflation means nominal spending targets shrink — but it coincided with collapsing asset values and credit contraction. Pair it with the Depression-era equity and bond figures in the next two tables, not as a standalone "good inflation" input. RRL accepts a negative inflation value (verified before publishing this version of the guide).

### A.4 — Equity returns by era (nominal)

Mean and SD are computed from annual S&P 500 (and predecessor index) total returns with dividends reinvested. Mean is converted to nominal from the real series using each era's CPI mean; standard deviation is essentially unchanged between real and nominal at the precision displayed.

| Era | Yrs | Mean % | SD % |
|---|---|---|---|
| Full history (1872–2022) | 151 | 10.9 | 18.0 |
| Great Depression (1929–1939) | 11 | 3.6 | 30.0 |
| WWII & postwar boom (1940–1965) | 26 | 14.9 | 18.1 |
| Stagflation (1966–1982) | 17 | 8.4 | 17.3 |
| Long bull market (1983–1999) | 17 | 18.9 | 12.5 |
| Lost Decade (2000–2009) | 10 | 1.4 | 20.1 |
| Post-GFC recovery (2010–2019) | 10 | 13.8 | 10.4 |
| Recent (2010–2022) | 13 | 13.1 | 13.1 |

**Key observations:**

- **The long bull market (1983–1999) should not serve as a planning baseline.** A nominal mean of 18.9% with SD of only 12.5% is historically exceptional. Plans calibrated to those parameters will be more optimistic than most historical experience warrants.
- **Stagflation was particularly damaging to decumulation portfolios.** Equities returned 8.4% nominal, which sounds fine — but pair it with 6.9% inflation and the real spending of a retired person grew faster than the portfolio. There was no single crash year and no recovery spike to rescue a sequence; the damage accumulated gradually over 17 years.
- **The Lost Decade produced a nominal mean of just 1.4%** — and that was against 2.5% inflation, so real returns were negative for a full decade. For someone taking withdrawals throughout, the sequence-of-returns risk compounded the damage.

### A.5 — Bond returns by era (nominal)

10-year US Treasury annual total returns, nominal, dividends/coupons reinvested.

| Era | Yrs | Mean % | SD % |
|---|---|---|---|
| Full history (1872–2022) | 151 | 5.2 | 8.8 |
| Great Depression (1929–1939) | 11 | 4.4 | 5.4 |
| WWII & postwar boom (1940–1965) | 26 | 2.5 | 5.3 |
| Stagflation (1966–1982) | 17 | 6.2 | 11.0 |
| Long bull market (1983–1999) | 17 | 10.5 | 10.7 |
| Lost Decade (2000–2009) | 10 | 6.9 | 7.9 |
| Post-GFC recovery (2010–2019) | 10 | 4.1 | 6.3 |
| Recent (2010–2022) | 13 | 2.6 | 9.1 |

**Key observations:**

- **During the Depression, bonds were protective.** Nominal bond returns averaged 4.4% — and deflation made fixed coupons more valuable in real terms. A blended portfolio held up considerably better than equities alone in that scenario.
- **The 2022 bond crash is included in the Recent era figures.** The recent era mean of 2.6% nominal reflects the full run from 2010 through 2022 including the rate-shock year.
- **Stagflation bonds returned 6.2% nominal**, which would have looked fine on a screen, but were eroded by 6.9% inflation — a slightly negative real return alongside the equally-poor real equity returns.

### A.6 — Equity / bond correlation by era

When you blend equity and bond assumptions, the degree of risk reduction depends on how correlated the two assets are. A negative correlation means bonds tend to rise when equities fall — meaningful diversification benefit. A positive correlation means they tend to move together — less benefit, and potentially no benefit if both decline simultaneously.

The correlation is **not stable across time**. Using a single fixed number for all scenarios produces era-inappropriate blended SD values.

| Era | Equity/bond correlation | n | Implication |
|---|---|---|---|
| Full history (1872–2022) | +0.164 | 151 | Mild positive — modest diversification benefit overall |
| Great Depression (1929–1939) | -0.331 | 11 | Negative — bonds partially offset equity losses |
| WWII & postwar boom (1940–1965) | +0.236 | 26 | Moderate positive — limited diversification benefit |
| Stagflation (1966–1982) | +0.293 | 17 | Positive — both assets declined together in real terms |
| Long bull market (1983–1999) | +0.598 | 17 | Strongly positive — both assets rose together |
| Lost Decade (2000–2009) | -0.928 | 10 | Strongly negative — bonds rose sharply as equities fell |
| Post-GFC recovery (2010–2019) | -0.200 | 10 | Mildly negative — modest cushioning effect |
| Recent (2010–2022) | +0.345 | 13 | Positive — diversification broke down in the 2022 rate shock |

### A.7 — Blending equity and bond assumptions

Given equity allocation `e` (as a decimal, e.g. 0.60 for 60%) and bond allocation `b = 1 − e`:

```text
blended_mean = e × equity_mean + b × bond_mean
blended_sd   = sqrt( e² × equity_sd² + b² × bond_sd² + 2 × e × b × equity_sd × bond_sd × correlation )
```

Use the **era-specific correlation** from A.6 for the scenario you are modeling. Correlation matters: a 60/40 mix during the Lost Decade was much less risky than the simple weighted sum of variances would suggest, because bond returns moved against equity returns.

#### Pre-computed 60/40 blends across allocations — Full history parameters

Equity (nominal): mean 10.9%, SD 18.0% · Bond (nominal): mean 5.2%, SD 8.8% · Correlation: +0.164

| Allocation (equity / bond) | Blended mean % | Blended SD % |
|---|---|---|
| 100 / 0 | 10.9 | 18.0 |
| 80 / 20 | 9.8 | 14.8 |
| 70 / 30 | 9.2 | 13.3 |
| 60 / 40 | 8.6 | 11.9 |
| 50 / 50 | 8.1 | 10.7 |
| 40 / 60 | 7.5 | 9.6 |
| 30 / 70 | 6.9 | 8.8 |
| 0 / 100 | 5.2 | 8.8 |

For era-specific blended values, use the formula above with the era's Mean / SD / Correlation rows.

### A.8 — Named stress-test scenarios

Each scenario below is a 60/40 mix using the era's equity, bond, and correlation values, with the era's mean CPI as the inflation input. Drop these into the form directly to run an "if this era happened again, does my plan survive?" check.

#### Scenario A — Long-run baseline (60/40)

A planning anchor reflecting the full 151-year history of US markets. Includes both favorable and unfavorable eras.

| Field | Value |
|---|---|
| Mean annual return | 8.6 % |
| Annual standard deviation | 11.9 % |
| Inflation rate | 2.3 % |

*Basis: full-history equity nominal mean 10.9% / SD 18.0%, bond nominal mean 5.2% / SD 8.8%, era correlation +0.164.*

#### Scenario B — Stagflation (60/40)

Seventeen years of persistently high inflation, mediocre nominal equity returns, and bonds that provided no real protection. A useful stress test for decumulation plans because the damage accumulated gradually.

| Field | Value |
|---|---|
| Mean annual return | 7.5 % |
| Annual standard deviation | 12.4 % |
| Inflation rate | 6.9 % |

*Basis: stagflation-era equity nominal mean 8.4% / SD 17.3%, bond nominal mean 6.2% / SD 11.0%, era correlation +0.293.*

#### Scenario C — Great Depression (60/40)

High equity volatility and severe drawdowns, offset by strong bond performance and deflation. The Depression-era equity/bond correlation was -0.331; bonds partially cushioned equity losses in a way they did not during stagflation.

| Field | Value |
|---|---|
| Mean annual return | 3.9 % |
| Annual standard deviation | 17.4 % |
| Inflation rate | -1.7 % |

*Basis: Depression-era equity nominal mean 3.6% / SD 30.0%, bond nominal mean 4.4% / SD 5.4%, era correlation -0.331.*

*Note: a negative inflation rate models deflation — your spending target shrinks in nominal terms each year. RRL accepts negative inflation; verified.*

#### Scenario D — Lost Decade (100% equity)

A full decade of slightly-positive nominal equity returns against 2.5% inflation — i.e. a negative real return. Presented as 100% equity because the bond behavior during this era (correlation -0.928, strong flight-to-safety) was historically unusual and modeling pure equity gives a more conservative picture without relying on that exceptional bond behavior repeating.

| Field | Value |
|---|---|
| Mean annual return | 1.4 % |
| Annual standard deviation | 20.1 % |
| Inflation rate | 2.5 % |

*Basis: Lost Decade equity nominal mean 1.4% / SD 20.1%.*

#### Scenario E — Long bull market (60/40)

The most favorable sustained era in the dataset. Useful as a reference for how sensitive your plan is to unusually favorable conditions, and as context for how much the other scenarios deviate from it. The high positive correlation (+0.598) means blending provided less volatility reduction than in other eras.

| Field | Value |
|---|---|
| Mean annual return | 15.5 % |
| Annual standard deviation | 10.6 % |
| Inflation rate | 3.3 % |

*Basis: long bull market equity nominal mean 18.9% / SD 12.5%, bond nominal mean 10.5% / SD 10.7%, era correlation +0.598.*

#### Scenario F — Post-GFC recovery (60/40)

The decade from 2010 to 2019. Low volatility, low inflation, solid equity returns, and a mildly negative equity/bond correlation. Does not include the 2022 rate shock.

| Field | Value |
|---|---|
| Mean annual return | 9.9 % |
| Annual standard deviation | 6.2 % |
| Inflation rate | 1.8 % |

*Basis: Post-GFC equity nominal mean 13.8% / SD 10.4%, bond nominal mean 4.1% / SD 6.3%, era correlation -0.200.*

### A.9 — Suggested stress-test workflow

The intent is the same regardless of how you run the simulation: save a baseline run, then run the same scenario with stress-test inputs and compare.

1. Enter your primary planning assumptions in the form. Tap **Run Simulation**.
2. Open the Library (bookcase icon) and **Save current draft as…** with a name like `baseline`. The result persists with the scenario, so you can re-open it later without re-running.
3. Edit the form to a stress-test scenario from A.8 — for Stagflation, set Mean annual return to 7.5%, Annual standard deviation to 12.4%, and Inflation rate to 6.9%. Keep the other inputs (Current age, Retirement age, End age, Annual retirement spending) aligned with your baseline so the comparison is apples-to-apples. Tap **Run Simulation**.
4. **Save current draft as…** another scenario, e.g. `stagflation`.
5. Tap the **Compare** toolbar button. Pick the saved scenario you want to overlay. The Survival and Balance Range tabs both render both curves; the dashed line is the comparison.
6. Repeat for the other A.8 scenarios you want to test (Great Depression, Lost Decade, Long bull market, etc.).

For a target-driven version — "what spending level meets 80% survival in the Stagflation scenario?" — use **Goal Seek** (target icon in the toolbar). Goal Seek runs a binary search and reports the suggested adjustment, then offers an Apply button.

The comparison workflow — not any single run in isolation — is where the analytical value of these scenarios concentrates.

### A.10 — Data sources and methodology

**Primary source:** Robert J. Shiller, *Stock Market Data Used in "Irrational Exuberance"* (updated dataset). Available at `http://www.econ.yale.edu/~shiller/data/ie_data.xls` and `http://shillerdata.com`. The version used to produce this guide covers January 1871 through September 2023 and includes monthly S&P 500 price, dividends, earnings, CPI, long-term interest rate, and derived real total-return series.

**Columns used from the Shiller dataset:**

| Column index | Column label | Used for |
|---|---|---|
| 4 | CPI | Annual inflation rate |
| 9 | Real TR Price | Annual real equity total return (converted to nominal here) |
| 18 | Real Total Bond Returns | Annual real bond total return (converted to nominal here) |

**Calculation method.** Annual returns are computed as December-to-December changes in the relevant index:

```text
annual_return(Y) = ( index(Dec, Y) / index(Dec, Y-1) ) − 1
```

producing 151 annual observations covering 1872 through 2022. Standard deviations are sample standard deviations (denominator n−1) across all annual observations within each era. Era-specific equity/bond correlations are Pearson coefficients across the annual return pairs within the era. Real-to-nominal conversion uses each era's mean CPI per the relation in A.1.

### A.11 — Disclaimer

The figures in this appendix are historical observations derived from a single dataset covering US markets. They are not forecasts. Past return distributions, volatility levels, correlation structures, and inflation regimes do not predict future outcomes.

These inputs are provided to help you explore how a plan calibrated to various historical conditions would perform under RRL's parametric normal Monte Carlo model. This is not the same as predicting which conditions will recur, in what sequence, or with what statistical properties.

Retirement Risk Lab outputs are planning analysis. They are not financial advice, investment recommendations, or guarantees of any outcome.

---

