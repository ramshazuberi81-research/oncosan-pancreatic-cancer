# Stage dominates prognosis and limits machine-learning gains in adolescent and young adult pancreatic neoplasms

A temporally validated SEER analysis of survival and 12-month mortality prediction in adolescent and young adult (AYA) patients with malignant pancreatic primaries, diagnosed 2004–2022.

**Author:** Ramsha Zuberi (ORCID [0009-0004-9272-0343](https://orcid.org/0009-0004-9272-0343))
**Status:** Manuscript in preparation

## Summary

- **Cohort:** 1,466 AYA patients (median age 27 y; 62.6% female) from a SEER*Stat export; 496 deaths (33.8%), median follow-up 39.5 months.
- **Survival:** 5-year survival 95.7% (localized), 68.0% (regional), 21.7% (distant).
- **Cox model:** distant vs localized stage HR 13.16 (95% CI 9.17–18.88); C-index 0.870.
- **Prediction:** 12-month mortality models (logistic regression, random forest, gradient boosting, mean-probability ensemble) trained on diagnoses before 2018 (n=834) and tested on 2018–2021 (n=433). Ensemble test AUROC 0.921 (0.888–0.949). Stage had by far the largest permutation importance (0.159).
- **Benchmark:** a stage-only logistic model (result: see manuscript).

## Repository contents

```
.
├── README.md
├── manuscript/
│   └── AYA_pancreatic_SEER_manuscript.docx
├── results/
│   ├── cohort_flow.csv              # Supplementary Table S1 (cohort derivation)
│   ├── table1.csv                   # Table 1 (characteristics by stage)
│   ├── km_summary.csv               # Kaplan–Meier summaries by stage
│   ├── cox_hazard_ratios.csv        # Table 3 / Figure 2 (Cox model)
│   ├── ml_results.csv               # Table 2 (model performance, feature sets A and B)
│   ├── permutation_importance.csv   # Figure 4
│   └── manuscript_numbers.txt       # headline numbers quoted in the text
├── figures/
│   ├── fig1_km_by_stage.png         # Figure 1
│   ├── fig2_cox_forest.png          # Figure 2
│   ├── fig3_roc_calibration.png     # Figure 3
│   └── fig4_feature_importance.png  # Figure 4
└── code/                            # analysis scripts / notebook (add here)
```

## Data

This repository contains **aggregate outputs only**. Patient-level SEER data are **not** included and may not be redistributed under the SEER Research Data Agreement.

To reproduce the analysis:

1. Request access to SEER research data from the NCI (<https://seer.cancer.gov/data/access.html>).
2. Export pancreatic primaries (site recode C25.x) with SEER*Stat. Record the database release, session settings and age restriction here: `[SEER release / session details]`.
3. Variables used: age (five-year groups), sex, race/ethnicity, year of diagnosis, SEER summary stage, grade, histology, tumor size, marital status, surgery, chemotherapy, survival months, vital status.

## Methods in brief

- **Inclusion:** malignant C25.x primaries, diagnosed 2004–2022, first or only primary, valid survival time, known age and sex (266,170 export records → 1,466 analyzed).
- **Survival:** Kaplan–Meier with log-rank test; multivariable Cox model (age, sex, diagnosis year, stage, grade, histology, race); Schoenfeld residuals for proportional hazards.
- **Prediction:** outcome is death within 12 months. Temporal split: train <2018, test 2018–2021. Feature set A (baseline variables); set B adds surgery and chemotherapy and is exploratory because of immortal-time bias. Decision threshold for 95% sensitivity is set on training out-of-fold predictions only. Bootstrap (500 resamples) confidence intervals. No survival-time, vital-status or cause-of-death variable is used as a predictor.
- **Reporting:** TRIPOD+AI.

## Environment

`[Python version]`, with `[package versions: lifelines / scikit-learn / pandas / numpy / matplotlib]`. Add a `requirements.txt` or `environment.yml` to `code/`.

```bash
pip install -r requirements.txt
python code/run_analysis.py --seer-export path/to/seer_export.csv
```

`[Replace with the actual entry point once the code is added.]`

## Limitations

SEER has no symptoms, laboratory values, imaging, family history or BMI. The study is prognostic, not diagnostic, and cannot evaluate screening. The temporal test set is small (48 deaths) with no external validation. Treatment variables are subject to confounding by indication and immortal-time bias.

## Citation

```
Zuberi R. Stage dominates prognosis and limits machine-learning gains in adolescent
and young adult pancreatic neoplasms: a temporally validated SEER analysis.
[Journal / preprint server, year; DOI]
```

## License

Code: `[e.g. MIT]`. Aggregate results and figures: `[e.g. CC BY 4.0]`.

## Contact

`[email]`
