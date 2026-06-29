# Retirement Risk Lab — User Guide

*For the macOS / iPadOS / iOS app, last updated 2026-06-21.*

This guide explains how to use Retirement Risk Lab, what every input on the form means, how to read the charts, and how to use the Lifetime tools (Library, Compare, Goal Seek, CSV export, backup/restore).

If you only have 90 seconds, jump to **[Quick start](#quick-start)**. If you want to understand why the chart says what it says, read **[Reading the results](#reading-the-results)**. If you want one specific number to use for an input, the **[Field-by-field guide](#the-form-field-by-field)** has historical anchors and source citations for every assumption.

Every field in the form has a tooltip in the app — hover (Mac) or tap the **ⓘ** icon (iPad / iPhone) next to any field for the short version of what's here.

---

## Why this app exists

When I retired in 2023, my wife and I had a Sunday ritual: "doing the money." I'd pull together all our account balances, plug them into a spreadsheet, and give her a rough sense of how long our savings might hold out. It worked, but I always knew it was just a best guess.

A proper retirement planner — the kind financial advisors use — runs thousands of "what if the market does something unexpected?" scenarios to estimate how likely your money is to last. I wanted that kind of analysis at home, on demand, without having to bother anyone.

So I built Retirement Risk Lab. It runs those thousands of scenarios for you and gives you a clear picture of where you stand.

---

## What the app actually does

Retirement Risk Lab runs a **Monte Carlo simulation** of your retirement. That's a fancy way of saying it plays out thousands of possible futures — same starting point, same plan, but different stock-market luck in each run — and tells you what fraction of those futures end with you still having money at the age you care about.

The headline answer looks like this:

> *There is a **62.4% chance** your money lasts to age 95.*

That's a probability, not a guarantee. The point of running thousands of futures is to give you a number that reflects market uncertainty rather than a single best-guess projection that pretends the market is predictable.

Think of it like a flight simulator for your retirement. No real money moves. You're just testing how your plan holds up under a wide range of conditions.

Your simulations and saved files stay on your device. The app doesn't send your run data anywhere unless you turn on iCloud sync, in which case the data travels only between *your* devices via your Apple ID's private CloudKit container.

---

## Quick start

1. **Open the app.** The form on the left (Mac / iPad) or top (iPhone) is pre-filled with a reasonable starting example: current age 55, retire at 62, end at 95, $1,000,000 starting balance, $20,000/yr contribution, $60,000/yr retirement spending, 5% mean return, 12% standard deviation, 2.5% inflation.
2. **Change the four numbers that matter:** *Starting balance*, *Annual retirement spending*, *Current age*, *End age*. Leave everything else alone for the first run. (Tip: if you paste from a spreadsheet cell formatted as currency — `$1,000,000` — the app accepts the dollar sign and commas automatically.)
3. **Tap Run Simulation.** Results appear in a couple of seconds.
4. **Read the headline** at the top of the results pane — it answers "will my money last to age N?"
5. **Tweak and re-run.** The simulator is fast; play with retirement age, spending, and starting balance to see what changes the answer. When you edit a field after a run, the results above turn into a "These results are out of date — re-run for current numbers" banner so you don't accidentally trust stale numbers.

That's the whole loop. On macOS and iPad, the window title shows the name of the loaded scenario from the Library (or "Untitled draft" when you're working from scratch), so you can tell at a glance which plan you're looking at.

The next sections explain the inputs and outputs in detail when you're ready.

---

## How the simulation works (the short version)

Each "trial" inside the simulation walks your portfolio forward, year by year, from your current age to your end age. In each year it:

1. Adds your annual contribution (if you haven't retired yet).
2. Draws a random return for that year, using your mean return and standard deviation as the shape of the distribution.
3. Applies the return to your portfolio.
4. Subtracts your spending (grossed up for taxes if enabled), the RMD floor (if applicable), and adds Social Security income (if it's started).
5. Records whether you still have money at the end of the year.

After all the trials finish, the app counts: *out of N futures, how many still had money at age 95?* That's your survival probability.

The randomness comes from one place: the per-year return draw. A "lucky" future has a string of good years; an "unlucky" one has a string of bad years (especially in the early retirement years — the so-called *sequence of returns* risk). Running thousands of trials means you sample the full range of lucky and unlucky paths, not just one.

---

## The form, field by field

The form is grouped into sections that mirror the parts of a retirement plan. You don't need to touch every field — most have sensible defaults — but understanding what each one does helps you trust the answer the simulator gives back.

### Person

- **Current age.** Your age today. Where the simulation starts on the timeline.
- **Retirement age.** The age you plan to stop working. Before this age, your contribution is added to the portfolio each year. From this age onward, your retirement spending (and Social Security if enabled) takes over.
- **End age.** How long you want your money to last. The headline answer is "the probability you still have money at this age." Pick an age you actually want to plan to — 95 is common; 100 is conservative.

### Portfolio

- **Starting balance.** Today's total across all your retirement accounts (401(k), IRA, taxable brokerage). Use pre-tax dollars; the tax gross-up handles withdrawals downstream.
- **Annual contribution (pre-retirement).** What you add to your accounts each year while you're still working. Stops at retirement age automatically. Set to $0 if you're already retired.

### Spending and inflation

- **Annual retirement spending.** Total dollars you'll spend per year in retirement, *before* taxes. The simulator grosses this up to a withdrawal amount when withdrawal tax gross-up is enabled (it is by default).
- **Inflation rate.** Yearly inflation. Your spending and Social Security benefits grow by this rate each year of the simulation. Over the last 30 years (1995–2024) US CPI inflation has averaged about **2.5%** per year. The Federal Reserve's stated long-run target is **2%** (measured by PCE). The full historical average since 1913 is higher — about **3.2%** — because it includes the 1970s and the post-WWII period. 2.5% is the default; pick higher if you're worried about a sustained period of elevated inflation. *(Source: BLS CPI-U; see [Sources](#sources).)*
- **Values are nominal.** A toggle. **Off** (default) means every dollar amount you typed in is in **today's** dollars, and the simulator inflation-adjusts them automatically. **On** means your inputs are already inflation-adjusted and won't grow over time — useful if you're comparing against a financial plan that already inflation-adjusted everything for you.

### Return model

This is where you tell the simulator how stocks behave. The defaults are reasonable for a balanced portfolio.

- **Mean annual return.** Your portfolio's average yearly nominal return. Historical anchors *(all nominal, with dividends/coupons reinvested)*:
  - **100% S&P 500: ~10% nominal long-run average.** Annualized CAGR ~9.8% since 1928 per the NYU Stern Damodaran dataset.
  - **60% stocks / 40% bonds: ~7–9% nominal.** Vanguard reports 8.8% annualized 1926–2021; CFA Institute reports 9.6% for 1972–2021; the trailing 10-year is around 7%.
  - **100% bonds: ~5% nominal long-run.** 10-year Treasuries returned ~4.9% CAGR since 1928 (Damodaran). The 2010s were notably lower as rates fell to near zero.
- **Annual standard deviation.** How bumpy the ride is. Higher volatility means a wider spread between "lucky" and "unlucky" futures. Anchors:
  - **100% S&P 500: ~15–20%.** Full history ~18.5%; trailing 50 years ~16%.
  - **60/40 balanced: ~10–12%.** Trailing 10-year closer to 8–9%.
  - **100% bonds: ~5–8%.** Long-run ~8% per the Damodaran dataset.

You can use this to model "what if I'm more conservative in retirement?" — drop the mean to 4–5% and the standard deviation to 7–8% to see how a conservative glidepath changes survival. *(Sources: NYU Stern Damodaran, Vanguard, CFA Institute — see [Sources](#sources).)*

### Social Security

- **Include Social Security.** Toggle that turns on a Social Security income stream starting at the age you specify. While the income is flowing, your portfolio withdrawal is reduced by that amount (less stress on the portfolio).
- **Start age.** When you start claiming. The earliest is **62** (with reduced benefits) and the maximum-benefit age is **70**. Your *Full Retirement Age* (FRA) depends on the year you were born: it's **67 for anyone born in 1960 or later**, and between 66 and 66 years 10 months for those born 1955–1959. Anyone born in 1954 or earlier has an FRA of 66. If you were born in 1943 or later, every year you delay claiming past your FRA increases your benefit by exactly **8%** (2/3 of 1% per month) up to age 70 — credits stop accruing after 70. *(Source: SSA Benefits Planner — see [Sources](#sources).)*
- **Annual benefit (at start age).** Your projected annual SS benefit at the start age you chose. Look this up at [ssa.gov/myaccount](https://ssa.gov/myaccount) — they have a personalized estimate based on your earnings history. Enter the **gross** annual benefit (the SSA-reported figure, before any withholdings). If your Medicare Part B/D/IRMAA premiums are being deducted from your monthly SS check, do not subtract them here — instead include them in your **Annual retirement spending** number. (Doing both, or doing neither, is the most common source of bad answers from this kind of planner. See the Healthcare section for the full warning and what the spending number should include.)
- **Annual COLA.** Social Security's cost-of-living adjustment. Since automatic adjustments began in 1975, COLAs have averaged about **3.7% per year**; the trailing 20-year average is closer to **2.6%**. Recent COLAs were 5.9% (2022), 8.7% (2023), 3.2% (2024), 2.5% (2025), and 2.8% (2026). Using your assumed long-run inflation rate is a reasonable simplification since COLAs track CPI-W. *(Source: SSA Office of the Chief Actuary — see [Sources](#sources).)*

### Taxes

- **Enable withdrawal tax gross-up.** On (default): your *spending* number is treated as the money you actually want to spend after taxes, and the simulator withdraws extra each year to cover the tax bill. Off: your spending number is treated as a tax-free withdrawal (e.g. all-Roth).
- **Effective withdrawal tax rate.** Your blended federal + state tax rate on retirement withdrawals. Per Fidelity's 2024 analysis of a $100,000 IRA withdrawal, blended effective rates run roughly **8–13% for married-filing-jointly retirees** and **14–20% for single filers**, depending heavily on state. The exact number depends on:
  - How much of your withdrawal is from Roth vs traditional (Roth is tax-free)
  - Whether you live in a no-income-tax state (FL, TX, NV, etc.) or a high-tax state (CA, NY, NJ, OR)
  - Total annual income (Social Security taxability and tax bracket)
  - Filing status (singles pay materially more than MFJ at the same gross income)

*(Source: Fidelity, "Best States to Retire for Taxes" — see [Sources](#sources).)*

### RMD (Required Minimum Distribution)

The IRS forces you to withdraw a minimum from traditional 401(k) / IRA accounts. Under the **SECURE 2.0 Act of 2022**, the start age is **73 if you were born between 1951 and 1959**, and **75 if you were born in 1960 or later**. People born in 1950 or earlier were already subject to age-72 or earlier rules. The RMD floor in the simulator enforces this: if your planned withdrawal in a given year is less than the RMD, the simulator withdraws the RMD amount instead.

- **Enable RMD floor.** On by default. Turn off if your money is all in Roth accounts (no RMDs).
- **Start age.** 73 for most current retirees (born 1951–1959); 75 for those born 1960 or later.
- **Annual rate.** Approximate withdrawal rate. Per the IRS Uniform Lifetime Table (in effect since 2022): about **3.8% at age 73**, **~5% at 80**, **~6.25% at 85**, **~8.2% at 90**, and **over 11% at 95**. Averaged across the 73–95 span, that's roughly **6–7% per year** (not 8% — the 8% figure applies near age 90). Use ~6.5% as a single-number default. *(Source: IRS Publication 590-B Appendix B Table III — see [Sources](#sources).)*

### Healthcare

The Healthcare field is a separate line for the cost of healthcare in retirement. The simulator treats it exactly the same way it treats Annual retirement spending — same inflation rate, same start age (retirement), same tax gross-up — and adds the two lines together to compute each step's withdrawal. So at the math level, splitting healthcare out or lumping it into spending makes no difference to the survival probability. These three scenarios produce identical results:

| Where you put healthcare | Annual retirement spending | Annual healthcare cost |
|---|---|---|
| Lumped into spending | $90,000 | $0 (toggle off) |
| Split out | $78,000 | $12,000 (toggle on) |
| Partial split | $85,000 | $5,000 (toggle on) |

Pick whichever feels cleaner to you. If you split, the Run Overview, Math tab, and stored result reflect the split exactly the way you typed it; nothing else changes.

The one mistake to avoid is **double-counting**: don't include the same dollars in both fields. If healthcare is already inside your $90K spending number, leave the Healthcare toggle off. If you turn the toggle on and enter $12K, your spending number should drop to $78K to compensate.

A future version of the simulator may give the healthcare line its own behavior — for example a separate medical-inflation rate (medical CPI has historically run roughly 1.5–2× general CPI), or an age-dependent step that drops the cost at 65 when Medicare kicks in. Whether either of those is worth adding depends on whether they meaningfully change planning outcomes versus a lumped estimate; we'll evaluate that based on use. For now, both fields behave identically and the choice is yours.

#### Sanity-checking your healthcare number

Whether you split it out or lump it into spending, this is what a realistic healthcare line should cover, with rough 2025 ranges. Use it as a reality check on whatever total you arrive at.

- **Medicare Part B premium** — ~$185/month standard 2025, indexed to medical-CPI. Withheld from your SS check (see the double-count warning below).
- **IRMAA surcharge** — $74–$443/month *additional* Part B premium for high-income retirees (modified AGI above ~$106K single / ~$212K MFJ in 2025). Plus a smaller Part D surcharge. Most retirees never see it.
- **Medigap supplement or Medicare Advantage** — Medigap Plan G is the most common supplement, $150–$300/month. Medicare Advantage often runs $0/month with network and prior-auth trade-offs.
- **Part D prescription drug coverage** — $30–$80/month for the plan plus copays and out-of-formulary drugs.
- **Dental, vision, hearing** — Original Medicare doesn't cover any of these meaningfully. A stand-alone dental plan runs $30–$60/month; vision and hearing are typically out-of-pocket.
- **Out-of-pocket deductibles, coinsurance** — most planners bake in $2,000–$5,000/year as a placeholder for "things that come up."
- **Pre-Medicare bridge (if retiring before 65)** — ACA marketplace plan net of subsidies, typically $400–$1,500/month per person. Dominates the healthcare line for early retirees. Vanishes at 65.
- **Long-term care** — most retirees self-insure. If you do carry LTC insurance, premiums are $2,000–$10,000/year depending on age at purchase, state, and policy.

Realistic totals to expect once you add it all up:

| Situation | Per-person annualized | Per couple |
|---|---|---|
| 65+ on Medicare + Medigap + Part D, no IRMAA, no LTC | $5,000–$8,000 | $10,000–$16,000 |
| 65+ on Medicare + Medigap + Part D, with IRMAA | $7,000–$13,000 | $14,000–$26,000 |
| Ages 60–64 on an ACA marketplace plan | $5,000–$18,000 | $10,000–$36,000 |
| Self-funded long-term care premium added on top | +$2,000–$10,000 | +$4,000–$20,000 |

If your Annual retirement spending implies a healthcare share well below these ranges, you may be under-budgeting. Well above, you may be over-budgeting (or carrying LTC insurance the table doesn't assume).

> **Avoid the Medicare-from-Social-Security double-count.** If your Medicare Part B (and Part D, and IRMAA surcharge) premiums are being withheld from your monthly Social Security check, the **Annual benefit (at start age)** you enter in the Social Security section should be your **gross** benefit (the SSA-reported amount before any withholding) — and your Annual retirement spending should include the Medicare premiums **once** as part of the healthcare share. Either:
> - Enter gross SS and include Medicare premiums in your spending number (recommended; matches how the SSA reports the number); or
> - Enter net-of-Medicare SS and exclude Medicare premiums from your spending number.
>
> What you must NOT do is enter gross SS *and* exclude Medicare from your spending — that gives you the premium for free. Or enter net SS *and* include Medicare in spending — that charges you twice.

### Simulation

- **Timestep.** **Annual** is what you want for the headline "will my money last to age N?" question. **Monthly** is useful when you want to know *which month* your portfolio runs out, not just which year. Monthly is a Lifetime Unlock feature.
- **Number of trials.** How many random futures to simulate. More trials = a tighter confidence interval but a slower run.
  - **5,000** (Free tier maximum): enough to see the trend, with a 95% confidence interval of about ±1 percentage point.
  - **200,000** (typical Lifetime choice): a tight answer, with a 95% confidence interval of about ±0.2 percentage points.
  - Anywhere from **50,000 to 200,000** is a sweet spot for most planning work.
  - **Lifetime ceilings differ by timestep.** Annual mode allows up to **2,000,000** trials. Monthly mode allows up to **410,000** trials for a typical retirement horizon, lower for longer spans. The reason is a memory-safety guard: monthly mode stores 12 checkpoints per year for the Balance Range fan chart and Path Table, so the maximum trial count that fits within a safe memory budget on iPad and iPhone is roughly `250,000,000 ÷ (months in the simulation)`. The Number of trials stepper enforces this automatically — its upper bound drops when you switch to monthly mode and rises when you switch back to annual.
- **Seed mode.** *Fixed* means same random numbers every run, so you can A/B-test changes (e.g. "what if I retire one year later?") without random noise polluting the comparison. *Random* means fresh random numbers each run, more like real-life uncertainty.
- **Seed.** Any whole number. The specific value doesn't matter; what matters is that two runs with the same seed produce the same results.

---

## Reading the results

The results pane has three pieces: the **headline**, the **Run Overview**, and the **four chart tabs** (Survival by Age, Balance Range, Path Table, Math). If you've edited any input since the last run, an orange **"These results are out of date"** banner sits above the headline to warn you that the numbers below were computed from a different scenario than the form currently shows. Tap Run Simulation to refresh; the banner clears and everything below updates together.

### The headline

> *There is a 62.4% chance your money lasts to age 95.*
>
> *About 37.6% of simulated futures ran out before then. Among futures that ran out, the typical run-out was around age 88; in the unluckiest 10% of futures, money ran out by age 81.*

Three numbers to read:

- **The big percentage.** Your survival probability at the end age you picked.
- **The typical run-out age.** Among the futures that DID fail, when (on median) the money ran out.
- **The unluckiest 10% run-out age.** Among the failed futures, the 10th-percentile bad-luck case. This is your "I really shouldn't be planning around this" floor.

### Run Overview

- **Trial quality.** `good` / `fair` / `low confidence`. Based on the confidence-interval half-width. `good` means your number is solid. `low confidence` means you should run more trials before trusting the headline.
- **95% CI half-width.** How wide the confidence interval around your survival probability is, in percentage points. A 1.0 pp half-width means "I'm 95% sure the true probability is within ±1.0 percentage points of the number I just told you."
- **Failed trials.** How many of your simulated futures ran out of money before the end age, expressed as `X of Y`.
- **Elapsed.** Wall-clock time the run took.
- **Seed.** The random seed used (for reproducing the run).

### Chart tabs

**Survival by Age** (the default and the most important tab):

- Blue line: percentage of simulated futures still solvent at each age. Read it like a fuel gauge over time.
- Orange band: the 95% confidence interval around the blue line. Wider band = noisier estimate. (Lifetime users can change the confidence level to 80% / 90% / 95% / 99%.)
- Vertical dashed rule: your target end age.
- Hover (Mac) or tap (iPad/iPhone) any point on the chart to see the exact age, survival percentage, and CI bounds.

**Balance Range** (the dollar view):

- Three lines: p10 (unlucky), p50 (typical), p90 (lucky) portfolio balance at each age.
- **Important caveat:** trials that ran out are counted at $0 in every later checkpoint. So the p10 line hitting $0 at age 80 means at least 10% of futures have failed by then. The p50 line hitting $0 means more than half have failed. A flat p50 line that never reaches $0 does NOT mean "you're safe" — it means more than half of futures still have money. For the actual "will my money last" answer, look at the Survival by Age tab.

**Path Table** (the row-by-row view):

- One row per checkpoint, with p10/p50/p90 balances and the change since the previous row.
- In annual mode the rows are by year (`age 66`, `age 67`, …); in monthly mode they're by month within year (`age 66m1`, `age 66m2`, …).
- Lifetime users can **Export CSV** from the toolbar above the table for analysis in Excel, Numbers, or Google Sheets. The default filename includes the seed and trial count so a downstream tool can tell two exports apart at a glance.

**Math** (the formulas behind the curves):

- A read-only transparency view: the canonical per-step operation order; the annual → step conversion formulas with your inputs substituted in (e.g. `step_mean = (1 + annual_mean)^(1/12) - 1 = 0.407412%`); the per-step balance equation; a worked example using your scenario's first retirement step; the Wilson 95% confidence-interval calculation broken down into `denom`, `center`, `radius`; and the nearest-rank percentile indices.
- The displayed Wilson CI bounds always agree with the Run Overview's `95% CI half-width` row to the digit — they're computed from the same engine helpers. If you've ever wondered "where exactly does that 42.04% come from?", this tab shows you, step by step.
- Useful when explaining the result to someone else, or when you want to sanity-check a hand calculation.

---

## Saved scenarios, sync, compare, and goal seek

These are Lifetime features.

### Library

Tap the **bookcase icon** in the toolbar to open the Library sheet. From there you can:

- **Save current draft as…** — give the current form values a name (e.g. *Retire at 60*, *Retire at 65*, *Spend $80K*) and store it.
- **Save changes to active scenario** — overwrite the named scenario you currently have loaded. Available from the Save menu when a library scenario is active.
- **Load** a saved scenario by tapping its row or the explicit **Load** button on the right edge. A blue checkmark on the row marks the scenario you currently have loaded; the button label changes to **Reload** for the active row so you can re-apply the saved values if you've edited the draft.
- **Rename** and **Delete** via the row's context menu (right-click on Mac, swipe on iPad/iPhone, or the trailing-edge actions).

When you load a scenario, the app restores **both the inputs and the last simulation result you saved with it**. You see the headline and charts the way they were the moment you saved, with no re-run required.

The window title (macOS / iPad) shows the loaded scenario's name so you can tell at a glance which plan you're looking at.

### iCloud sync

Saved scenarios sync to all your devices signed in to the same Apple ID. The sync uses **Apple's private CloudKit container** — your scenarios are stored encrypted under your account, and Apple's privacy guarantees apply (no one but you, including the developer, can read them). To turn it off, sign out of iCloud system-wide; there's no separate switch inside the app.

The Settings sheet has a **Scenario Backup** section (Lifetime only) for users who want a file-based copy alongside (or instead of) CloudKit sync:

- **Export scenarios to file…** writes every saved scenario — inputs, last result, timestamps — into a single JSON file. Default filename includes the date so multiple exports stay organized.
- **Import scenarios from file…** merges the file into the library. Newer copies in the file replace older copies on the device (last-write-wins on the modification timestamp), so re-importing a backup is safe and idempotent.

The backup file is the one thing the app keeps stable for the long haul — it's a versioned JSON envelope, so a file you export today will still import cleanly into a future version. Use this if you ever want to move scenarios between Apple IDs, share a plan with a spouse on a different account, or just want an off-device safety net.

### Compare

Tap the **two-rectangles icon** in the toolbar after running a primary simulation. Pick a saved scenario from the sheet; the Survival by Age and Balance Range tabs both gain a second overlay curve, with the dashed line representing the compared scenario.

If the saved scenario already has a stored result (the normal case, because results are saved with scenarios), the overlay appears **instantly** — no re-run, no waiting. If the scenario has never been run, the app runs it in the background, shows a "Running the comparison scenario…" banner above the headline, and writes the result back to the library so the next Compare against the same scenario is also instant.

### Goal Seek

Tap the **target icon** in the toolbar to find the smallest scenario adjustment that hits a target survival probability. Two modes:

- **Lower retirement spending** — finds the highest annual spending that still meets your target.
- **Raise retirement income (Social Security)** — finds the lowest SS benefit that would meet your target. Useful when modeling "how much would I need to bring in from a part-time job to make 80% work?"

Pick a target survival probability (e.g. 80%), choose a mode, tap **Run goal seek**. Goal Seek does a binary search through up to 24 candidate values, reports the suggested number, and offers an **Apply to scenario** button that drops the value into your form. The internal trial count is normalized to a runtime-friendly range so the search returns in seconds even on monthly mode.

---

## Lifetime Unlock

Retirement Risk Lab is fully free for the core question: *will my money last?* Lifetime Unlock ($24.99 one-time, Family Sharing included) adds the deeper-analysis features:

- **Named scenario library** — Save as many scenarios as you want, reload them later, rename or delete from a single sheet.
- **iCloud sync across devices** — Your scenarios follow you between Mac, iPad, and iPhone via Apple's private CloudKit container.
- **Scenario Backup** — Export every saved scenario (with its last result) to a single JSON file, and import the file back to restore. A self-contained safety net that's independent of iCloud.
- **Compare two scenarios** — Overlay a saved scenario's survival curve and balance lines on the current chart. Instant when the saved scenario already has a stored result.
- **Goal Seek** — Find the smallest scenario adjustment (lower spending or raise SS benefit) that hits a target survival probability. Binary search returns in seconds.
- **Monthly timestep** — Find which *month* the portfolio runs out, not just which year.
- **Trial count up to 2,000,000 (annual) / 410,000 (monthly)** — Tightest possible confidence interval; the monthly ceiling is lower to keep memory safe on iPad and iPhone.
- **Adjustable confidence level** — Choose 80% / 90% / 95% / 99% on the survival chart.
- **Path CSV export** — Take the checkpoints into your own analysis tools.

You can buy Lifetime Unlock from any of the lock icons in the form or from the Settings sheet (gear icon in the toolbar). **Restore Purchases** is always reachable from Settings, even before purchase (App Store requirement).

---

## Suggested settings

These are starting points organized by **planning posture**. They're not prescriptions — your situation may justify different numbers — but they give you a defensible default for every field and let you change one or two values intentionally without having to research every other number yourself.

Every value below is sourced from the same datasets cited in the field-by-field guide (BLS for inflation, NYU Stern Damodaran for equity/bond returns, SSA for COLA, IRS for RMD rates, Fidelity 2024 study for taxes). See **[Sources](#sources)** for the underlying citations.

For full *historical-era* stress-test scenarios (Stagflation, Great Depression, Long Bull Market, etc.) with mean/stddev/inflation combinations derived from the Shiller dataset, see **[Historical assumptions reference](historical-assumptions.md)** (also reproduced as Appendix A at the bottom of this document). This section is for everyday planning postures; that one is for era-specific stress tests.

### Optimistic posture

For: someone who wants a "if things go well-ish, am I fine?" baseline. Don't plan exclusively on this; pair with the Moderate or Pessimistic posture for a realistic range.

| Field | Suggested | Why |
|---|---|---|
| Mean annual return | 8% | Slightly above the long-run 60/40 mean (~7–8%) — assumes mildly favorable equity returns. |
| Annual standard deviation | 10% | Mid-range of historical 60/40 (~10–12%); cleaner sequences than full history. |
| Inflation rate | 2.0% | Federal Reserve PCE target. |
| Annual COLA (if Social Security on) | 2.0% | Match the inflation assumption. |
| Effective withdrawal tax rate | 10% | Lower end of MFJ-retiree range (~8–13%). |

### Moderate posture (recommended baseline)

For: most users. This is the "what should I expect on average?" default and the closest fit to the typical retiree's experience.

| Field | Suggested | Why |
|---|---|---|
| Mean annual return | 7% | Mid-range of long-run 60/40 (~7–9%). |
| Annual standard deviation | 11% | Mid-range of long-run 60/40 standard deviation. |
| Inflation rate | 2.5% | Trailing 30-year US CPI-U average. |
| Annual COLA | 2.5% | Match inflation; recent 20-year SSA COLA average is 2.6%, close enough. |
| Effective withdrawal tax rate | 12% | Mid-range of MFJ-retiree blended fed+state rates per Fidelity 2024. |

### Pessimistic posture

For: stress-testing. "If things go meaningfully worse than the historical average, does my plan still hold up?" Use this alongside Moderate to see how much of your survival probability depends on benign conditions.

| Field | Suggested | Why |
|---|---|---|
| Mean annual return | 5% | Conservative glidepath / bond-heavy mix. |
| Annual standard deviation | 8% | Lower-volatility mix that pairs with the lower mean return. |
| Inflation rate | 4.0% | Midpoint between recent and stagflation-era means; protects against a sustained-elevated-inflation regime. |
| Annual COLA | 4.0% | Match inflation. |
| Effective withdrawal tax rate | 15% | Upper end of MFJ-retiree range, or a typical single-filer's bottom-of-range. |

### Stress-test posture

For: "is my plan robust to a genuinely bad regime?" This isn't a recommendation to plan for; it's a sensitivity check.

| Field | Suggested | Why |
|---|---|---|
| Mean annual return | 3% | Below long-run bond CAGR; a sustained negative-real-return regime for equities. |
| Annual standard deviation | 18% | Approximating full-history S&P 500 standard deviation. |
| Inflation rate | 6.9% | Full Stagflation-era CPI mean. |
| Annual COLA | 6.9% | Match inflation. |
| Effective withdrawal tax rate | 18% | Upper end of single-filer range, or a high-tax-state MFJ retiree. |

### Equity-mix shortcut

If you don't want to think about postures and just want defaults that match a specific stock/bond allocation, use these — same values referenced in the field-by-field guide, gathered here for quick lookup.

| Allocation | Mean return | Standard deviation |
|---|---|---|
| 100% S&P 500 | 10% | 18% |
| 80% stocks / 20% bonds | 9% | 15% |
| 60% stocks / 40% bonds | 7% | 11% |
| 40% stocks / 60% bonds | 6% | 9% |
| 20% stocks / 80% bonds | 5% | 8% |
| 100% bonds | 5% | 8% |

These are nominal-return numbers, with dividends/coupons reinvested. They pair with whatever inflation rate you've set; do NOT also adjust them downward for inflation (that would double-count).

### Trial count shortcuts

| If you want… | Use |
|---|---|
| A quick sanity check while exploring | 5,000 trials, annual, fixed seed |
| A defensible answer to "will my money last?" | 50,000–200,000 trials, annual, fixed seed |
| The tightest possible confidence interval | 2,000,000 trials, annual |
| Depletion month, not just year | 50,000–100,000 trials, monthly |
| Monthly with the tightest interval the engine allows | Up to 410,000 trials, monthly (the form's stepper enforces this) |

---

## Frequently asked questions

**Why does my Free run have a wider confidence interval than my Lifetime friend's?**

The Free tier caps trials at 5,000; Lifetime allows up to 2,000,000. More trials → tighter interval. Both tiers give you the right answer; Lifetime just gives you more decimal places of precision.

**Why does the p50 balance line never reach $0?**

Depleted trials are floored at $0 in every later checkpoint. So the p50 line only reaches $0 if *more than half* of all simulated futures have run out. If a third of futures fail by age 90, the p50 line at 90 is the median balance of the remaining two-thirds — still way above $0.

**What does "nominal" vs "real" dollars mean?**

Nominal = future-year dollars (what you'll actually pay for groceries in 2050). Real = today's dollars (purchasing-power adjusted). By default, the simulator treats your inputs as today's dollars and grows them by inflation automatically — that's the right setting for almost every user. The toggle exists for users who've already done the inflation math themselves.

**The "Failed trials" number includes futures where I died of old age before running out — is that a problem?**

No. The simulator runs your portfolio all the way to End age regardless of life expectancy; "failed" means "ran out of money before End age", not "died with money still in the account". If you survive past End age, that's a financial-planning success on this simulator's terms.

**My results changed when I re-ran with the same inputs. Why?**

You're in *Random* seed mode. Switch to *Fixed* and set a specific seed if you want the same result every time. Random mode is useful if you want to see the natural variation; Fixed mode is useful if you want to A/B test changes ("what if I retire one year later?") without random noise polluting the answer.

**Is the math sound?**

The simulation uses standard quantitative-finance assumptions: normally-distributed annual returns (Box-Muller draws from a normal distribution, applied to portfolio balance), nearest-rank percentiles for the path balance curves, and Wilson binomial confidence intervals for the survival probabilities. The code is open source; you can read every line in the GitHub repo.

**Will the app work without an internet connection?**

Yes. The simulation runs entirely on your device. The only network-dependent features are iCloud sync (Lifetime, optional) and the in-app purchase / Restore Purchases flow.

**Does the app collect any data about me?**

No. The app sends nothing about your inputs, results, usage, or device anywhere. Apple's App Store sees the purchase event for Lifetime Unlock; that's it. See the [privacy policy](https://retirementrisklab.app/privacy) for the full statement.

---

## Sources

The numeric defaults and historical anchors quoted in this guide and in the in-app tooltips were validated against the following authoritative public sources. Where a range is quoted, the underlying source is one of these; where a single number is quoted as a default, it reflects the source's headline figure for a retirement-planning audience.

**Inflation**
- US Bureau of Labor Statistics — [Consumer Price Index (CPI-U) historical data](https://www.bls.gov/cpi/data.htm). Long-run geometric mean since 1913: ~3.2%; trailing 30 years (1995–2024): ~2.5%.
- Federal Reserve — official PCE inflation target of 2%, set 2012, reaffirmed annually.
- Reference compilation: [usinflationcalculator.com — Historical Inflation Rates 1914–present](https://www.usinflationcalculator.com/inflation/historical-inflation-rates/).

**Equity, bond, and balanced-portfolio returns**
- NYU Stern, Aswath Damodaran — [Historical Returns on Stocks, Bonds and Bills: 1928–Current](https://pages.stern.nyu.edu/~adamodar/New_Home_Page/datafile/histretSP.html). S&P 500 total return CAGR ~9.8%, std dev ~18.5%. 10-year US Treasuries CAGR ~4.9%, std dev ~8.2%.
- Vanguard Institutional — [The global 60/40 portfolio: steady as it goes](https://institutional.vanguard.com/insights-and-research/perspective/the-global-60-40-portfolio-steady-as-it-goes.html). US 60/40 annualized 8.8% over 1926–2021.
- CFA Institute Research and Policy Center — [Performance of the 60/40 portfolio](https://rpc.cfainstitute.org/research/reports/2025/performance-of-the-60-40-portfolio). 60/40 (S&P 500 + intermediate Treasuries) annualized 9.61% over 1972–2021; std dev 9.51%.

**Social Security**
- SSA Office of the Chief Actuary — [Cost-of-Living Adjustments](https://www.ssa.gov/oact/cola/colaseries.html). Annual COLA history since 1975; average ~3.7%.
- SSA — [2026 COLA announcement of 2.8%, dated 24 Oct 2025](https://www.ssa.gov/news/en/press/releases/2025-10-24.html).
- SSA Benefits Planner — [Full Retirement Age by birth year](https://www.ssa.gov/benefits/retirement/planner/ageincrease.html). 67 for those born 1960+; sliding scale 66–66+10mo for 1955–1959.
- SSA Benefits Planner — [Delayed Retirement Credits](https://www.ssa.gov/oact/quickcalc/early_late.html). 2/3 of 1% per month, exactly 8% per year, for those born 1943+.

**Retirement taxes**
- Fidelity Learning Center — [Best States to Retire for Taxes](https://www.fidelity.com/learning-center/personal-finance/best-states-to-retire-for-taxes). Blended fed+state effective rates for a $100K IRA withdrawal: 7.81%–12.98% MFJ; 13.93%–20.41% single.

**RMD rules**
- IRS Publication 590-B — [Distributions from Individual Retirement Arrangements (IRAs)](https://www.irs.gov/publications/p590b), Appendix B Table III "Uniform Lifetime Table" (in effect since 2022).
- SECURE 2.0 Act of 2022 — start-age timeline: 73 for those born 1951–1959; 75 for those born 1960 or later. Congressional Research Service [In Focus IF12750](https://www.congress.gov/crs-product/IF12750).

**Confidence-interval math**
- The 95% half-widths quoted in this guide for n=5,000 and n=200,000 trials are computed directly from the Wilson score interval for a binomial proportion. The engine uses Wilson — see `ios/RRLEngine/Sources/RRLEngine/Stats.swift` in the repo for the implementation.

If you find a number in this guide or the in-app tooltips that doesn't match these sources, please file an issue.

---

## Appendix A — Historical assumptions reference

*Also available as a standalone page at [Historical assumptions reference](historical-assumptions.md). Same content.*

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

## Support

- **App version:** see *Settings → About* for the exact build.
- **Privacy policy:** [retirementrisklab.app/privacy](https://retirementrisklab.app/privacy)
- **Help home:** [retirementrisklab.app/help](https://retirementrisklab.app/help)

Retirement Risk Lab is published by Eddie Merkel.
