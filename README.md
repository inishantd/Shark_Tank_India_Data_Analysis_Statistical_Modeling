# Shark Tank India — Data Analysis & Statistical Modeling

Analysis of Shark Tank India (Seasons 1–2): data
cleaning, exploratory analysis, hypothesis testing, and two interpretable
models, capped off with an analysis-ready export that powers a 3-page
Power BI dashboard.

## Dataset

Pitch-level data for Shark Tank India Season 1 (Dec 2021 – Feb 2022) and
Season 2 (Jan–Mar 2023): 321 pitches, 74 columns covering the ask (amount,
equity, implied valuation), whether an offer was received/accepted, final
deal terms, and per-shark investment amounts for the 8 sharks who appear in
these two seasons (Ashneer, Namita, Anupam, Vineeta, Aman, Peyush, Ghazal,
Amit). Sourced from a public GitHub mirror of the show's episode data
([Siddharth-94/EDA-On-Shark-Tank-India-Data](https://github.com/Siddharth-94/EDA-On-Shark-Tank-India-Data)).


## Notebook structure

1. Business Problem / Objective
2. Dataset Overview
3. Data Cleaning & Preparation — dtype fixes, one data inconsistency
   corrected, ask/valuation math verified, outlier handling, derived columns
4. Exploratory Data Analysis — conversion rates, deal-size distribution,
   season/shark/industry breakdowns, ask vs. deal scatter plots, correlation
   heatmap
5. Business Questions
6. Statistical Analysis — 11 hypothesis tests (chi-square, Mann-Whitney U,
   Kruskal-Wallis + post-hoc, Spearman correlation, one/two-proportion
   z-tests, bootstrap CI), each with H0/H1, assumption checks, effect size,
   and a plain-English interpretation printed from the actual computed
   result (nothing hand-typed)
7. Statistical Modeling — logistic regression (deal / no-deal) and
   log-linear regression (deal amount), with leakage-safe predictors,
   odds ratios, R², and residual diagnostics
8. A/B-Style Analysis — low vs. high valuation ask, and low vs. high equity
   offered, explicitly labeled observational (not a randomized experiment)
9. Key Business Insights — descriptive vs. statistically significant vs.
   non-significant findings, generated from the combined
   Benjamini-Hochberg–corrected results table
10. Final Interactive Dashboard Preparation — exports the two CSVs in
    `outputs/` and specifies the 3-page Power BI layout
11. Final Conclusions — executive summary, strongest findings, limitations,
    and what cannot be concluded from observational data

## Headline findings

- **321 pitches, 176 deals — 54.8% conversion rate.**
- Deal size is right-skewed (median ₹50 lakh vs. mean ₹63 lakh); one
  extreme outlier ask (₹300 crore) was kept and flagged rather than dropped.
- **Ask amount is the strongest driver of deal amount** (Spearman ρ = 0.66,
  p < 0.001; log-linear regression R² = 0.61).
- **Season 2 converted significantly better than Season 1** (62.7% vs.
  46.1%, p = 0.007 after correction) — the one factor that held up as a
  significant predictor of deal odds in the logistic regression.
- Industry, which shark, valuation-ask level, and equity offered did
  **not** show a statistically significant effect on deal success once
  corrected for multiple testing, despite visible gaps in the raw charts.
- The logistic regression's weak discriminative power (test AUC ≈ 0.54)
  says the same thing from a different angle: pitch paperwork alone
  explains little of who gets a deal — most of the signal likely lives in
  the in-studio pitch itself, which this dataset doesn't capture.

Full statistical detail (test statistics, p-values, effect sizes,
confidence intervals) is in Section 6 of the notebook; the corrected
summary table is in Section 9.

## Power BI dashboard

`outputs/sharktank_pitches_clean.csv` and `outputs/sharktank_shark_deals_long.csv`
are the two tables the dashboard is built from; `sharktank_dashboard_theme.json`
is a ready-to-import dark theme. The 3-page design (Executive Overview,
Shark Investment Strategy, Startup & Deal Analysis) is specified in
Section 10 of the notebook.

## Limitations

- Only 2 seasons / 321 pitches — several subgroup tests have small sample
  sizes once split.
- Financial fields (revenue, margins) are missing for most pitches.
- This is edited television, not a controlled data-collection process —
  correlations here should not be read as causal.

## Tech stack

Python 3.11 · Pandas · NumPy · SciPy · Statsmodels · scikit-learn ·
Matplotlib · Seaborn · Plotly · Jupyter
