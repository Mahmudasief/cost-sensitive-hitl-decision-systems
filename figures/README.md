# Figures

This directory contains all generated figures for the paper.

## Contents

| File | Description |
|---|---|
| `cost_vs_threshold_rf.png` | Total cost vs classification threshold — Random Forest |
| `cost_vs_threshold_lr.png` | Total cost vs classification threshold — Logistic Regression |
| `hitl_regime_heatmap.png` | HITL regime map: % of configurations where HITL beats baseline, by human review cost and false-negative cost |
| `fig1_class_imbalance.png` | Class distribution in the credit card fraud dataset |
| `fig2_amount_distribution.png` | Transaction amount distribution by class |
| `fig3_fraud_rate_by_amount.png` | Fraud rate by transaction amount bucket |
| `fig4_correlation_heatmap.png` | Feature correlation heatmap |

## How Figures Were Generated

All figures are generated from the notebooks in `notebooks/`:

- EDA figures (fig1–fig4): `01_eda.ipynb`
- Cost-vs-threshold plots: `02_baseline_models.ipynb`
- HITL regime heatmap: `02_baseline_models.ipynb` (sensitivity analysis section)

Figures are committed here for reference and paper submission.
