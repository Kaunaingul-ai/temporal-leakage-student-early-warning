# Temporal Data Leakage in Explainable Student Early-Warning Models

**Research title:** Temporal Data Leakage in Explainable Student Early-Warning Models: Effects on Performance, SHAP Attributions, and Class Errors

## Overview

This repository provides the experimental notebooks, figures, and evaluation results supporting a research study on temporal data leakage in educational early-warning models.

The study investigates how information unavailable at the intended prediction time can influence predictive performance, SHAP-based feature explanations, and class-specific classification errors.

Experiments use the Open University Learning Analytics Dataset (OULAD) and compare temporally valid (leakage-free) models with deliberately leakage-contaminated models.

## Research Objectives

The study examines three hypotheses:

- **H1 — Predictive performance:** Temporal leakage inflates apparent predictive performance, particularly at early course-progress cutoffs.
- **H2 — Model explanations:** Temporal leakage changes feature-attribution patterns, increasing the apparent importance of information unavailable at prediction time.
- **H3 — Class-specific errors:** Improved aggregate performance under leakage does not necessarily imply improved discrimination between Fail and Withdrawn outcomes.

## Dataset

**Dataset:** Open University Learning Analytics Dataset (OULAD)

**Reference:** Kuzilek, J., Hlosta, M., & Zdrahal, Z. (2017). Open University Learning Analytics Dataset. *Scientific Data, 4*, 170171.

Dataset source: https://analyse.kmi.open.ac.uk/open_dataset

The study considers four student-outcome categories:

1. Distinction
2. Pass
3. Fail
4. Withdrawn

Experiments evaluate predictions at four course-progress cutoffs: **10%, 20%, 30%, and 40%**.

The leakage-free condition restricts features to information available at the relevant prediction cutoff. The leaky condition deliberately permits post-cutoff information to investigate the effects of temporal boundary violations.

## Modelling Approach

Two classification algorithms are evaluated:

- Multinomial Logistic Regression
- XGBoost

The modelling workflow incorporates:

- Student-level train–test separation
- Group-aware cross-validation
- Training-fold preprocessing
- Median imputation for numerical variables
- Most-frequent imputation for categorical variables
- One-hot encoding of categorical variables
- Hyperparameter selection using cross-validation
- Consistent experimental comparisons between leakage-free and leaky conditions

The experimental random seed is **42**.

## Evaluation

Model evaluation includes:

- Accuracy and balanced accuracy
- Macro-averaged F1-score
- Per-class precision, recall, and F1-score
- Multiclass log loss and Brier score
- Calibration assessment
- Confusion matrices and normalized class-error analysis
- Paired bootstrap sensitivity analysis
- Fixed-cohort sensitivity analysis

The analysis places particular emphasis on confusion between the Fail and Withdrawn outcome categories.

## Explainability Analysis

SHAP is used to evaluate feature-attribution patterns under leakage-free and leaky modelling conditions.

Features are also examined using conceptually defined feature families, including assessment-related, engagement-related, and static/background information.

SHAP results are interpreted as model attributions rather than causal effects.

## Main Findings

The experiments indicate that:

1. Temporal leakage inflates apparent predictive performance, with particularly large effects at early prediction cutoffs.
2. The relative importance of assessment-related information increases when post-cutoff features are permitted.
3. Improved aggregate classification metrics can coexist with increased normalized confusion between Fail and Withdrawn outcomes.
4. Fixed-cohort sensitivity analysis supports the persistence of leakage-associated performance inflation beyond differences in evaluation-cohort composition.

These findings highlight the importance of temporally valid feature construction, evaluation, and interpretation in educational early-warning systems.

## Repository Structure

```text
temporal-leakage-student-early-warning/
|
|-- notebooks/
|   Research notebooks
|
|-- figures/
|   Research figures and supplementary visualizations
|
|-- results/
|   Evaluation outputs and sensitivity analyses
|
|-- requirements.txt
|   Python dependency specifications
|
|-- README.md
```

## Software Environment

The recorded modelling environment includes:

| Software | Version |
|---|---|
| Python | 3.12.13 |
| pandas | 2.2.2 |
| NumPy | 2.0.2 |
| scikit-learn | 1.6.1 |
| XGBoost | 3.3.0 |

Additional dependencies are documented in `requirements.txt`.

## Reproducibility

To reproduce or inspect the experimental workflow:

1. Obtain the OULAD dataset from the official source.
2. Download or clone this repository.
3. Install the dependencies listed in `requirements.txt`.
4. Open the notebooks in Google Colab or a compatible Python environment.
5. Configure the notebook paths to the local OULAD data and output directories.
6. Follow the preprocessing, modelling, evaluation, and explainability workflows.

The notebooks may require their Google Drive paths to be adapted before execution in another environment.

Saved results and figures are provided for inspection and comparison.

## Interpretation and Limitations

The deliberately leaky modelling condition is an experimental intervention designed to assess the effects of temporally invalid feature availability. It should not be interpreted as a recommended operational modelling approach.

The study is based on OULAD, and external validation would be necessary before generalizing its findings to other institutions or learning environments.

The SHAP findings describe predictive model behaviour and do not establish causal relationships between individual features and student outcomes.

## Research Status

This repository accompanies a research manuscript undergoing revision. Results and documentation should be considered in conjunction with the corresponding manuscript and supplementary materials.

## Data Availability

The OULAD dataset is available through its original public source. The original dataset is not redistributed through this repository.

## License

No reuse license is declared here. Repository contents remain subject to applicable copyright and the original dataset's terms of use.

Document reviewer sensitivity analyses.

## Fixed-Cohort Sensitivity Analysis

To assess whether changes in evaluation-cohort composition influenced the observed temporal leakage effects, an additional fixed-cohort analysis was conducted using the same 5,026 held-out student–module registrations, representing 4,626 unique students, at all four course-progress cutoffs (10%, 20%, 30%, and 40%).

Previously fitted Logistic Regression and XGBoost models were evaluated under leakage-free and deliberately leaky conditions. Performance was compared using accuracy, balanced accuracy, macro-F1, and normalized Fail–Withdrawn confusion.

The leakage-associated accuracy differences remained positive across all four cutoffs:

| Course cutoff | XGBoost gain (pp) | Logistic Regression gain (pp) |
|---|---:|---:|
| 10% | 14.66 | 11.26 |
| 20% | 12.06 | 9.69 |
| 30% | 10.01 | 7.86 |
| 40% | 7.96 | 6.71 |

These findings indicate that the observed leakage-associated performance differences were not explained solely by changes in the evaluation cohort across prediction cutoffs.

### Result Files

- `reviewer_fixed_cohort_full_results.csv` — Performance metrics for both algorithms and leakage conditions at all four cutoffs.
- `reviewer_fixed_cohort_differences.csv` — Paired performance differences in percentage points.

The registration-level cohort-key file is not included in this public repository to avoid redistributing student identifiers.
