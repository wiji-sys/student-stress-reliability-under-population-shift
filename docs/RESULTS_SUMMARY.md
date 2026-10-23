# Results Summary

## IID / LOSO

- IID group-blind ROC-AUC: **0.8657**
- LOSO ROC-AUC: **0.8547–0.8618**
- Recall at threshold 0.50: **0.4777–0.6871**

## Calibration

- Uncalibrated global Brier: **0.12974**
- Uncalibrated global NLL: **0.40865**
- Post-hoc calibration produced no consistent overall improvement in proper scoring rules.

## GroupDRO / threshold adaptation

- Fixed-threshold weighted ERM recall: **0.5917**
- Source-derived Recall≥0.80 threshold weighted recall: **0.7960**
- Worst-group recall: **0.4777 → 0.6902**
- Intervention rate: **24.9% → 40.9%**

## Conformal prediction

At 90% nominal coverage:

- Marginal weighted overall coverage: **0.9004**
- Marginal weighted high-stress coverage: **0.7468**
- Mondrian weighted high-stress coverage: **0.8984**
- Paired high-stress coverage improvement: **0.1490**

## Capacity-constrained screening

RiskTopK:

- K=10%: Precision@K **0.8598**, Recall@K **0.2963**, Lift@K **2.96**
- K=25%: Precision@K **0.7134**, Recall@K **0.6057**

## Robustness / leakage audit

- Seed ROC-AUC range: **0.86552–0.86592**
- Full model ROC-AUC: **0.86573**
- `Exam_Pressure` only: **0.81337**
- Full minus `Exam_Pressure`: **0.66873**
- 20 target permutations: mean ROC-AUC **0.4995** (range **0.4861–0.5056**)
