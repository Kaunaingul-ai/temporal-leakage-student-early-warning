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
