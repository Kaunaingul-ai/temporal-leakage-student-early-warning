# Reproducing the data-preparation pipeline

This repository release provides **source code**, not an independently validated clean-run environment. The published notebooks have their saved execution outputs removed; this does not change their computational steps.

## Inputs and order

1. Obtain the OULAD dataset from its official distribution and respect the dataset licence. Place original CSV files in `data/` under your project folder.
2. In Google Colab, mount Drive when applicable, then either use the default `/content/drive/MyDrive/AI_Research_Paper_1` layout or set `os.environ["OULAD_PROJECT_DIR"] = "/path/to/project"` **before** executing the first code cell.
3. Run notebooks `01_OULAD_Data_Audit`, `02_Temporal_Feature_Engineering`, `03_Leakage_Free_Dataset_Assembly`, and `04_Leaky_Dataset_Construction` in this order. Their `results/` and `processed/` outputs are inputs to the later training and explanation notebooks.
4. The repository model-training and SHAP reviewer-revision notebooks still have their own path conventions; review/configure their paths before running.
5. `07_Final_Results_and_Figures` is a **legacy result compilation**, and its historical table numbers and some figures are superseded by the manuscript reviewer-revision results. Do not substitute its older plots for the final manuscript figures.

## Methodological disclosures

- Assessment-feature availability uses a submission / assessment-due-date operational proxy. Actual grade-release times were not measured. This limitation must be stated consistently in the manuscript.
- Notebook 03 includes sequential correction and repeated assembly steps. Preserve the execution order; do not treat arbitrary cells as independently runnable.
- Do not upload raw or derived registration-level data without reviewing OULAD redistribution terms and the contents.
- The files here have passed JSON parsing and Python syntax compilation where applicable, **not** a fresh end-to-end execution with OULAD.
- The 05 and 06 reviewer notebooks should be audited separately for secrets, output disclosure, and dependencies.

- ## Reviewer Sensitivity Analyses

Notebook `08_Reviewer_Sensitivity_Analyses.ipynb` contains the additional experiments supporting the revised manuscript.

### Independent Hyperparameter Tuning

XGBoost hyperparameters were optimized independently for leakage-free and leaky datasets at 10%, 20%, 30%, and 40% course-progress cutoffs. Each experiment evaluated 15 candidate configurations using three-fold student-grouped cross-validation and macro-F1 as the selection criterion.

Results: `results/independent_tuning_all_cutoffs.csv`

### Feature-Family Ablation

Four conditions were evaluated using the original frozen XGBoost hyperparameters and identical student-level training and testing partitions: leakage-free, assessment-only leakage, VLE-only leakage, and combined leakage.

Results:
- `results/ablation_all_cutoffs.csv`
- `results/Table_Feature_Family_Leakage_Contributions.csv`

These files provide aggregate performance metrics and support Supplementary Tables S2 and S3.

### Computational Environments

The original environment record lists Python 3.12.13, pandas 2.2.2, NumPy 2.0.2, scikit-learn 1.6.1, and XGBoost 3.3.0.

The environment inspected during reviewer-sensitivity analysis used Python 3.13.16, pandas 2.2.3, NumPy 2.1.3, scikit-learn 1.6.1, XGBoost 3.4.1, and SHAP 0.52.0.

Reproduction requires configuring input paths, obtaining OULAD under its applicable terms, and executing the required preceding data-preparation and modelling steps. The available notebooks and results have not yet been independently validated through a complete clean-environment reproduction run.
