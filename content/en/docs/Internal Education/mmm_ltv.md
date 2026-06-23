---
title: "Validating the MMM with a geo experiment: does the recommended mix hold LTV steady?"
linkTitle: "MMM Customer-Quality Validation"
weight: 20
description: >
  A causal case study. Our Marketing Mix Model recommended reallocating spend.
  Before scaling it, we ran a geo-randomized matched-market experiment to test
  whether the new mix acquires MORE customers WITHOUT eroding their lifetime
  value (LTV) — read out with both Synthetic Difference-in-Differences and a
  Bayesian counterfactual, then audited at 12 and 18 months.
---

{{% pageinfo %}}
This page is a **teaching artifact** for the experimentation curriculum. It walks one test
end to end — **design doc → simulated run → readout** — on a fully synthetic dataset
(geo-week panel + a customer-level cohort audit). Every figure is computed from the attached
data (`data/geo_week_panel.csv`, `data/cohort_audit.csv`) and is reproducible from the scripts
(`scripts/generate_data.py`, `scripts/analysis.py`). The retailer "Lumen & Co." is fictional;
all numbers are synthetic.
{{% /pageinfo %}}

| | |
|---|---|
| **Experiment ID** | EXP-2025-118 |
| **Owner** | Growth / Marketing Science |
| **Window** | ~19 weeks kickoff → primary readout · confirmatory audits at month 12 & 18 |
| **Design** | 3-cell geo-randomized matched-market (DMA-level) |
| **Status** | **VALIDATED — SCALE THE MMM-RECOMMENDED MIX** |

## TL;DR for stakeholders

Our MMM recommended shifting spend toward a new channel mix. The worry: chasing volume often
means buying *cheaper, lower-quality* customers, so total revenue rises while per-customer LTV
quietly erodes. We tested it causally. **The MMM-recommended mix (Cell A) acquired ~9% more
customers while per-customer LTV stayed flat — comfortably inside our ±5% "no-erosion" band —
and the 12- and 18-month realized-revenue audit confirmed the quality held.** Pushing the same
channels 20% harder (Cell C) bought a little more volume but eroded LTV ~6%, so the MMM's
recommended point is already well-positioned. **Scale the reallocation; do not over-push.**

| Result | Cell A · MMM-recommended | Cell C · MMM +20% (stress) |
|---|---|---|
| **New-customer volume** (superiority) | **+9.2%** (90% CI +4.6 to +13.8) ✅ incremental | +11.8% (+7.2 to +16.4) |
| **Per-customer pLTV** (equivalence, ±5% ROPE) | **+0.5% to +2.4%** — inside ROPE ✅ no erosion | **−4.7% to −6.4%** — breaches ROPE ⚠️ |
| **12 & 18-month realized revenue** | **+1.6%** — stable, surrogate confirmed ✅ | −5.8% — erosion is durable, not noise |

---

# Part 1 · Pre-test design doc

## 1.1 The pain point — two correlated dashboards

Our MMM (a top-down Bayesian regression on aggregate spend and revenue) recommended moving
budget into a new channel mix. Today we have two trend lines — spend allocation and customer
LTV — that *move together*, but correlation is not causation. We cannot tell the executive team
whether the MMM-recommended mix is actually acquiring **higher-quality** customers, or simply
**more** customers of *lower* average value while the dashboard looks fine.

The originally proposed validation — suppress media to a control group identified by Customer
ID — cannot answer this. It would compare loyal high-value customers (the holdout) against
everyone else (the treated), so the groups differ *before* any media runs. That is selection
bias by construction, and it is made worse by the reality that CID-based suppression now matches
only 40–60% of profiles (Apple ATT, cookie deprecation) and cannot touch offline channels (CTV,
out-of-home, linear TV) at all.

> **In plain terms:** if your "control group" is your best customers and your "test group" is
> everyone else, any difference you measure is mostly *who they already were*, not *what the ads
> did*.

## 1.2 Hypothesis & the bet

> **Hypothesis.**
> **IF** we implement the channel-mix recommendations of our MMM,
> **THEN** we will acquire incrementally more customers while the per-customer lifetime value
> stays stable (within a ±5% practical-equivalence band),
> **WITHOUT** eroding customer quality — and that stability will hold when audited against
> realized revenue at 12 and 18 months.

This is a **stability / non-erosion** question, not a "make LTV go up" question. So our primary
read is an **equivalence test**: can we *rule out* a meaningful drop in per-customer LTV?

## 1.3 Experiment design — randomize geographies, not people

The unit of randomization must match the unit of decision-making. The MMM allocates spend at an
aggregate, geographic, weekly level, so the experiment randomizes whole **DMAs** (designated
market areas), not individuals. This single choice fixes every flaw of the CID design at once:
each cell contains a natural mix of loyal, occasional, and brand-new customers; privacy/identity
degradation is irrelevant because we measure aggregate regional outcomes; and the *entire*
omnichannel mix (including offline) can be turned up or down by geography.

{{< figure src="https://github.com/Officialyi/docsy/blob/main/content/en/docs/Internal%20Education/fig1_design.png?raw=true" alt="Three-cell geo-randomized design" width="680" >}}

| Cell | Allocation | Geos | Role |
|---|---|---|---|
| **A · MMM-recommended** ⭐ | The mix the MMM recommends | 15 DMAs | Treatment — the operating hypothesis |
| **B · Pre-MMM baseline** | The historical allocation, today's creative | 15 DMAs | Control — the proper counterfactual |
| **C · MMM +20%** | MMM mix, +20% on the highest-uncertainty channel | 10 DMAs | Saturation stress test |

Geos are not hand-picked: a power simulation (à la Meta GeoLift / Google `matched_markets`)
selects the assignment that maximizes power for the target effect, and the assignment is **locked
and pre-registered** before launch.

## 1.4 Metrics, guardrails & the decision rule

| Role | Metric | Test | Direction |
|---|---|---|---|
| **Primary** | Cohort pLTV per acquired customer (geo-week) | **Equivalence** vs ±5% ROPE | stay inside the band |
| **Co-primary** | New-customer volume | **Superiority** | higher is better |
| Co-primary (model-free) | 90-day realized revenue / customer | tracks the surrogate | stable |
| Confirmatory | 12- & 18-month realized revenue (locked cohort) | durability audit | stable |

**Pre-registered decision rule.** *Scale the MMM mix* if (a) the per-customer pLTV effect's
**90% interval lower bound sits above −5%** — i.e., we can rule out a meaningful erosion — under
**both** estimators, **and** (b) new-customer volume is incremental (90% interval excludes zero).
A cell **fails** the quality bar if its interval breaches −5%.

> **What's a ROPE?** A *region of practical equivalence* — a "close enough to flat" band we
> agree on before the test. Here ±5%. The goal isn't to prove LTV rose; it's to prove it didn't
> meaningfully fall.

## 1.5 How we'll read it — two estimators, in plain terms

We run **two independent causal estimators** and only trust a conclusion both support.

**1. Synthetic Difference-in-Differences (primary).** We build a *synthetic twin* of the treated
markets from a weighted blend of the control markets — the blend that moved in lockstep with the
treated markets *before* launch. After launch, the gap between the real markets and their
synthetic twin is the causal effect. We pressure-test it with **placebos**: pretend the switch
happened in control markets (where nothing actually changed) and confirm the method finds ~zero.

**2. Bayesian counterfactual (CausalImpact-style).** We use the control markets to *forecast what
the treated markets would have done* had nothing changed, and report the effect as a probability
distribution — e.g., "a 100% chance the per-customer LTV change is inside our ±5% band." A
Bayesian read answers the decision-maker's question directly: *how likely is erosion, and how big
could it be?*

A **panel difference-in-differences** serves as a third sensitivity check. (Why two-plus methods?
A geo experiment has few units and one shot — agreement across methods is how we earn trust.)

## 1.6 Population, randomization & timeline

- **Eligible unit:** a DMA on the national footprint; newly acquired customers are tagged at first
  transaction with their geo's cell and scored against a **locked** pLTV model (committed with a
  hash before launch — no retraining mid-flight).
- **Randomization:** whole DMAs, matched on pre-period trends, climate, and category seasonality;
  cells hold a natural population mix, so baseline equivalence holds by construction.
- **Timeline:** ~19 weeks kickoff → primary readout — a 12–26 week pre-period for matching, 3–4
  weeks design/pre-registration, **8 weeks active treatment** (enough for ad platforms to exit
  learning and for the consideration cycle + adstock to play out), a **4-week observation window**,
  then analysis. **Confirmatory audits at month 12 and month 18** verify the early surrogate read.

## 1.7 Power & the surrogate read

True 3-year LTV can't be observed in a test window, so we read out at T+90 days using a **locked
surrogate index** — a model validated on cohorts acquired ≥18 months ago that maps early behavior
to long-horizon value, reported *alongside* model-free 90-day realized revenue as a backstop.
Power is by simulation (bootstrapping historical geo-weeks); for per-customer pLTV the detectable
effect runs ~5–15% with 10–15 treatment DMAs, which is why ±5% is set as the practical-equivalence
threshold rather than something finer.

---

# Part 2 · Simulated run & analysis

## 2.1 The data

`geo_week_panel.csv` — 40 DMAs × 28 weeks (1,120 rows): cell assignment, geo covariates, and three
outcomes per geo-week (cohort pLTV/customer, new customers, 90-day realized revenue/customer).
`cohort_audit.csv` — ~100k customers in the locked treatment-window cohort, each with a predicted
pLTV and realized revenue at 90 days, 12 months, and 18 months. All estimators run on per-DMA
*normalized indices* (each market relative to its own pre-period), so markets of very different
size are comparable and the placebo null stays tight.

## 2.2 Credibility first — does the synthetic twin track?

Before reading any effect, we confirm the synthetic control tracks the treated markets in the
pre-period. It does; the two lines move together until launch, then separate:

{{< figure src="https://github.com/Officialyi/docsy/blob/main/content/en/docs/Internal%20Education/fig2_synthetic_fit.png?raw=true" alt="Synthetic control pre-period fit" width="620" >}}

## 2.3 Primary read — per-customer pLTV held steady (no erosion)

All three estimators put the per-customer pLTV effect for **Cell A** at essentially flat and
**inside the ±5% ROPE**:

| Estimator | Cell A effect | 90% interval | Read |
|---|---|---|---|
| Synthetic DiD | **+0.5%** | −1.1% to +2.2% | inside ROPE |
| Bayesian counterfactual | **+2.4%** | +1.6% to +3.2% | P(inside ROPE) = 100% |
| Panel DiD | **+0.6%** | 0.0% to +1.1% | inside ROPE |

The Bayesian posterior sits entirely within the no-erosion band, with **zero posterior mass below
−5%**:

{{< figure src="https://github.com/Officialyi/docsy/blob/main/content/en/docs/Internal%20Education/fig3_bayes_posterior.png?raw=true" alt="Bayesian posterior of pLTV effect vs ROPE" width="620" >}}

The estimators bracket the effect between +0.5% and +2.4% — they differ in magnitude (the
Bayesian read is a touch higher) but **agree unanimously on the decision**: per-customer quality
did not erode.

{{< figure src="https://github.com/Officialyi/docsy/blob/main/content/en/docs/Internal%20Education/fig4_estimators_forest.png?raw=true" alt="Estimator comparison forest plot" width="660" >}}

## 2.4 Co-primary — the volume *is* incremental

The reallocation acquired **+9.2% more new customers** in Cell A (90% CI +4.6% to +13.8%, interval
excludes zero). So the win is real and the right shape: **more customers at unchanged per-customer
quality.** The model-free 90-day realized revenue per customer moved +0.7% — tracking the surrogate
and confirming the pLTV read isn't an artifact of the model.

{{< figure src="https://github.com/Officialyi/docsy/blob/main/content/en/docs/Internal%20Education/fig6_volume_quality.png?raw=true" alt="Volume vs quality by cell" width="700" >}}

## 2.5 Falsification — placebos find nothing

Applying the synthetic-DiD machinery to control markets (where nothing changed) yields a null
distribution centered on zero. Cell A's effect sits squarely inside it (it is *not* distinguishable
from zero — exactly what "stable" should look like), while Cell C's −6.4% is far in the tail:

{{< figure src="https://github.com/Officialyi/docsy/blob/main/content/en/docs/Internal%20Education/fig5_placebo.png?raw=true" alt="Placebo distribution" width="620" >}}

## 2.6 The stress test — Cell C buys volume by eroding quality

Pushing the highest-uncertainty channel 20% harder than the MMM recommends got **+11.8%** volume —
only marginally more than Cell A — but per-customer pLTV fell **−4.7% to −6.4%**, breaching the −5%
ROPE on the synthetic-DiD and panel-DiD reads. The optimizer is already near the right point on the
response curve; over-spending pulls in lower-value marginal customers.

## 2.7 Durability audit — the surrogate held at 12 and 18 months

The whole readout rests on a 90-day surrogate for 3-year LTV, so the locked cohort was re-checked
against *realized* revenue. The surrogate's verdict held at every horizon: **Cell A stable at
≈+1.6%** through 18 months; **Cell C's erosion persisted at ≈−5.8%** — confirming it was a real
quality effect, not early noise.

{{< figure src="https://github.com/Officialyi/docsy/blob/main/content/en/docs/Internal%20Education/fig7_durability.png?raw=true" alt="Durability audit across horizons" width="640" >}}

And the customer-quality distribution itself barely moves between control and Cell A — the lift came
from *more* customers, not a shift in *who* they are:

{{< figure src="https://github.com/Officialyi/docsy/blob/main/content/en/docs/Internal%20Education/fig8_quality_distribution.png?raw=true" alt="Customer quality distribution" width="620" >}}

---

# Part 3 · Experiment readout

## 3.1 Verdict & the learning

**Scale the MMM-recommended allocation (Cell A) across the footprint.** It satisfied the
pre-registered rule on both counts — per-customer pLTV stayed inside the ±5% no-erosion band under
all three estimators, and new-customer volume was clearly incremental — and the 12/18-month audit
confirmed the quality is durable.

> **Learning: the MMM passed the test that matters — it grew volume without diluting quality.**
>
> The fear with any "spend more / spend differently" recommendation is that the extra customers are
> cheaper customers. They weren't. Equally important, the **+20% stress cell shows the limit**: push
> the same channels harder than the MMM recommends and you *do* start trading quality for volume.
> The optimizer is well-positioned; the recommendation is to execute it, not to exceed it.

## 3.2 What we ship

1. **Roll out the MMM-recommended mix** to the full footprint; retire the pre-MMM allocation.
2. **Hold at the recommended level — don't over-spend.** Cell C is the evidence that more is not
   better past the MMM's point.
3. **Calibrate the MMM with this result.** Inject the geo-lift posterior as a Bayesian prior on the
   relevant channel coefficient(s) in the next MMM refit — calibrating against the *immediate-response*
   component only, so we don't bias the model against the slow-building brand effect.
4. **Keep the audit commitment.** The 12/18-month realized-revenue read on the locked cohort stays on
   the calendar; it is what converts a surrogate estimate into a defended LTV claim.

## 3.3 Next experiments & honest limitations

- **Phase 2 — channel-level cadence.** This validated the *aggregate* mix, not every channel
  coefficient. A cadence of ~2 channel experiments/quarter refreshes MMM priors over time.
- **Geo spillover biases toward null.** National TV/search and cross-DMA travel leak across borders,
  so the true effect is likely *at least* what we measured (a conservative floor).
- **pLTV is a forecast.** We mitigated with a locked, back-tested surrogate, a model-free co-primary,
  and the realized-revenue audit — but the surrogate paradox is a known risk and is why the audit is
  non-negotiable.
- **External validity.** A mix tested at one shift size may not extrapolate to much larger shifts;
  the response curve is nonlinear (which is exactly what Cell C illustrates).

## 3.4 Reproduce / challenge this

```bash
python3 scripts/generate_data.py   # writes data/geo_week_panel.csv + data/cohort_audit.csv
python3 scripts/analysis.py        # SDiD + Bayesian + DiD + placebo, figures, results JSON
```

Change the ROPE, swap the donor pool, or re-seed the data and see whether the decision holds. A
healthy readout invites exactly that.

---

# Appendix

## A.1 Data dictionary — `geo_week_panel.csv`

| Column | Description |
|---|---|
| `dma`, `region`, `market_size_idx` | Geographic unit and covariates |
| `cell` | `control_baseline` · `mmm_recommended` · `mmm_plus20` |
| `week`, `period` | −15…12 (0 = last pre-week); `pre` / `treatment` / `observation` |
| `new_customers` | Newly acquired customers in the geo-week (volume metric) |
| `cohort_pltv_per_customer` | Surrogate pLTV per acquired customer (primary metric) |
| `realized_rev_90d_per_customer` | Model-free 90-day realized revenue / customer (co-primary) |

## A.2 Data dictionary — `cohort_audit.csv`

| Column | Description |
|---|---|
| `customer_id`, `dma`, `cell` | Locked treatment-window cohort |
| `predicted_pltv` | Surrogate model's prediction at acquisition |
| `realized_rev_90d` / `_12mo` / `_18mo` | Realized revenue at each audit horizon |

## A.3 Methods & sources

- **Synthetic DiD:** simplex-constrained synthetic-control weights matched on the pre-period, a
  DiD-adjusted post gap, and placebo permutation across control DMAs for the 90% interval (Arkhangelsky
  et al., 2021; Abadie et al. synthetic control).
- **Bayesian counterfactual:** conjugate Bayesian regression of the treated series on its
  best-correlated control DMAs, posterior-predictive counterfactual forward (CausalImpact-style;
  Brodersen et al., 2015). 60k posterior draws.
- **Panel DiD:** two-way fixed-effects change-in-means with a geo bootstrap.
- **Equivalence/ROPE & decision rule** pre-registered; surrogate-index readout follows Athey, Chetty,
  Imbens & Kang (2019); MMM calibration follows Meridian / Robyn / PyMC-Marketing lift-prior practice.

---

*EXP-2025-118 · MMM Customer-Quality Validation · Synthetic teaching dataset · Growth Experimentation
curriculum. "Lumen & Co.", all geographies, customers, and outcomes are fabricated for education.*
