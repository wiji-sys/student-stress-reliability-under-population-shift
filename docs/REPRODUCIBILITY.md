# Reproducibility Notes

## Execution order

1. E0–E2
2. E3
3. E4
4. E5
5. E6
6. E7
7. Reviewer leakage audit (independent)

The `MASTER_E0_E7_Full_Experiments.ipynb` notebook combines stages 1–6 in this order.

## Randomness

The core experiments use `random_state=42` unless an explicit seed-sensitivity grid is being evaluated. E7 evaluates seeds 1, 7, 21, 42, 84, 123, 202, 314, 512, and 777.

## Leakage controls

- Imputation, scaling, and one-hot encoding are fit only on training data.
- Calibration mappings are fit from source/inner OOF probabilities only.
- Source-derived thresholds use source OOF predictions only.
- Conformal quantiles use source calibration data only.
- Held-out-domain labels are used only for final evaluation, except explicitly labelled non-deployable oracle diagnostics.

## Statistical interpretation

Bootstrap CIs and paired Wilcoxon analyses are used as resampling-stability diagnostics. Repeated CV folds and repeated target evaluations are not independent population samples, and three LOSO domains are not treated as a basis for confirmatory population-level inference.
