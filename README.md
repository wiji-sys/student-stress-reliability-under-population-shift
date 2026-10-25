# Reliable Student Stress Prediction under Population Shift

Reproducibility repository for the study **“Reliable Student Stress Prediction under Population Shift”**

The repository contains the complete E0–E7 experimental pipeline, precomputed outputs, publication figures/tables, and the reviewer-requested `Exam_Pressure` leakage audit.

## Repository structure

```text
.
├── notebooks/
│   ├── 01_E0_E1_E2_Reliability.ipynb
│   ├── 02_E3_Calibration_Under_Population_Shift.ipynb
│   ├── 03_E4_ERM_vs_GroupDRO_Threshold_Adaptation.ipynb
│   ├── 04_E5_Conformal_Selective_Abstention_LOSO.ipynb
│   ├── 05_E6_Capacity_Constrained_Intervention_Policy.ipynb
│   ├── 06_E7_Robustness_Statistical_Synthesis.ipynb
│   ├── 07_Reviewer_ExamPressure_Leakage_Audit.ipynb
│   └── MASTER_E0_E7_Full_Experiments.ipynb
├── outputs/
│   ├── E0_E2/
│   ├── E3/
│   ├── E4/
│   ├── E5/
│   ├── E6/
│   ├── E7/
│   └── reviewer_audit/
├── data/
│   └── README.md
├── docs/
│   ├── RESULTS_SUMMARY.md
│   └── REPRODUCIBILITY.md
├── requirements.txt
├── CITATION.cff
└── .gitignore
```

## Dataset

The dataset itself is **not redistributed in this repository**. Download the public Kaggle dataset:

> S. Lavanya, *Student Lifestyle and Stress Prediction Dataset*, Kaggle.  
> https://www.kaggle.com/datasets/sridevilavanyacse/student-lifestyle-and-stress-prediction-dataset

Save the CSV as:

```text
data/student-lifestyle-and-stress-dataset.csv
```

Expected columns:

```text
Student_Type, Sleep_Hours, Study_Hours, Social_Media_Hours,
Attendance, Exam_Pressure, Family_Support, Month, Stress_Level
```

## Environment

The experiments were validated with Python 3.13.5, pandas 2.2.3, and scikit-learn 1.8.0.

```bash
python -m venv .venv
source .venv/bin/activate        # Linux/macOS
# .venv\Scripts\activate         # Windows
pip install -r requirements.txt
jupyter lab
```

## Recommended execution

For a complete clean rerun, open:

```text
notebooks/MASTER_E0_E7_Full_Experiments.ipynb
```

and use **Restart Kernel → Run All**.

The master notebook writes results to the matching folders under `outputs/`. E7 depends on outputs created by E0–E6, so the master notebook should be run sequentially from the top in a clean checkout.

For targeted reruns, use the numbered standalone notebooks. The reviewer audit is independent of E0–E7 and can be rerun separately.

## Experiment map

| Stage | Purpose |
|---|---|
| E0 | Data quality, missingness, plausibility, duplicates, population prevalence |
| E1 | Repeated IID baseline |
| E2 | Leave-One-Student-Type-Out population shift |
| E3 | Uncalibrated vs sigmoid vs isotonic calibration |
| E4 | ERM vs GroupDRO and source-derived threshold adaptation |
| E5 | Marginal vs Mondrian conformal prediction and selective abstention |
| E6 | Capacity-constrained intervention policies |
| E7 | Robustness, statistical inference, sensitivity analyses, publication synthesis |

## Key reproducibility notes

- `Student_Type` is excluded from the primary group-blind predictive feature set and is used as a domain/group variable in population-shift experiments.
- All preprocessing is fitted within the relevant training partition.
- Target-domain labels are evaluation-only for deployable LOSO procedures. Target-oracle analyses are explicitly diagnostic and non-deployable.
- Classical split-conformal guarantees require exchangeability. LOSO target-domain coverage is therefore reported empirically rather than as a formal target-domain guarantee.
- The public benchmark does not disclose the exact target-generation mechanism; the reviewer audit rules against deterministic target copying and obvious computational leakage but cannot eliminate construct overlap with an undocumented generator.

## Included outputs

The **FULL** repository package includes all generated outputs, including row-level prediction files. The **LIGHT** package excludes the largest row-level prediction CSVs while retaining summary tables, statistical results, figures, manifests, and all notebooks.

## Citation

See `CITATION.cff` for repository citation metadata.
