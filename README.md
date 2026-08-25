# Evaluating and Optimizing Machine Learning Models to Predict Drug Side Effects

**Vyas Koduvayur · Jenna Jabourian · Melody Mao · Flicka Zhang · Abeni Liu**

[View Research Paper](https://escholarship.org/uc/item/7343k6z4#main)

---

## Overview

Predicting drug side effects is an important challenge in pharmacology and drug development. Machine learning (ML) approaches can help identify patterns in large-scale drug and clinical datasets that may be difficult to detect using traditional methods.

In this project, we extend previous work by Liu and Wilson that used machine learning models to predict common drug-induced side effects using domain knowledge features including:

1. **Drug targets (DT)**
2. **Anatomical Therapeutic Chemical (ATC) classification codes**
3. **PathFX protein-protein interaction networks**

The original study found that Logistic Regression (LR) performed particularly well for side effect prediction, with models incorporating drug targets and level 2 ATC codes as the strongest-performing feature sets.

We investigated two extensions to the original work:

1. **ATC code granularity** — Does using more specific ATC classifications (levels 3–5) improve prediction accuracy?
2. **Model optimization** — Can fine-tuning the Logistic Regression model improve its predictive performance?

Our results suggest that increasing feature specificity does not necessarily improve model performance. ATC levels 2, 3, and 4 performed comparably, while level 5 substantially underperformed, likely due to overfitting. In contrast, fine-tuning the Logistic Regression model through decision-threshold optimization and regularization improved prediction accuracy across all 30 side effects examined. Notably, our fine-tuned model achieved higher predictive accuracy than the best-performing model reported in the original study, demonstrating that optimizing model parameters can improve performance even without introducing additional feature sets.

Together, these findings highlight the importance of balancing feature granularity, model optimization, and generalizability when applying machine learning to drug side effect prediction.

---

## Research Questions

Our analysis focused on two major questions:

* Does increasing the specificity of ATC classification codes from levels 2 through 5 improve drug side effect prediction?
* Can optimization of Logistic Regression parameters improve predictive accuracy beyond the original model?

---

## Methods & Analysis

The repository contains the code, datasets, intermediate results, and figure-generation scripts used for our analysis.

### ATC Code Analysis

We compared Logistic Regression models using **ATC levels 2, 3, 4, and 5** to determine how feature granularity affects predictive performance across the 30 most common drug-induced side effects.

We used ANOVA and pairwise statistical comparisons to evaluate differences between ATC levels, with additional comparisons between levels 2 and 4.

### Logistic Regression Optimization

We fine-tuned the Logistic Regression model by adjusting:

* **Decision threshold**, optimized using Youden's J statistic
* **Regularization strength (`C`)**, optimized using grid search
* **Maximum iterations**, increased to accommodate model convergence

The optimized model was then applied to the **DT/ATC feature combination**, using level 4 ATC codes.

### Code & Figures

* **`main_code.ipynb`** — Python code from the original study.
* **`main_code_modified.ipynb`** — Modified version of the original code, with sections not relevant to our project removed and new analysis added.
* **`main_code_tunedLR.ipynb`** — Modified version incorporating our fine-tuned Logistic Regression model.
* **`Figure Generation/Figures.Rmd`** — R Markdown script used to generate the figures presented in our project.

---

## Key Findings

Our analyses identified several important patterns:

* **ATC levels 2, 3, and 4 performed comparably**, suggesting that increasing ATC specificity does not necessarily improve predictive accuracy.
* **ATC level 5 substantially underperformed** the other levels, likely because its greater specificity resulted in sparse features and increased overfitting.
* **Level 2 and level 4 ATC models especially did not differ significantly** in overall prediction accuracy, both with and without drug-target features.
* **Fine-tuning Logistic Regression improved accuracy across all 30 side effects.**
* The fine-tuned model improved mean accuracy by approximately **0.0186** for the DT-only feature set.
* The final fine-tuned **DT/ATC model using level 4 ATC codes** achieved a mean accuracy of **0.7016**.
* Model optimization alone was able to outperform the original DT/ATC model for several individual side effects, demonstrating that **model optimization can be as important as adding additional domain-knowledge features**.

Overall, our results demonstrate a tradeoff between **feature specificity and model generalizability**, while showing that careful parameter optimization can improve drug side effect prediction.

---

## Data & Resources

### Original Study

This project extends the work of Liu and Wilson:

> *"Drug target, class level, and PathFX pathway information share utility for machine learning prediction of common drug-induced side effects."*

The original study's code is available through the [original GitHub repository](https://github.com/jenwilson521/ML_Atc_DT_PFX).

### Datasets Used

The following datasets and resources were used to reproduce and extend the original analysis:

1. **SIDER 4.1**

   [SIDER Download](http://sideeffects.embl.de/download/)

   * `meddra_all_se.tsv` — Contains drug-side effect associations curated using MedDRA classifications.
   * `drug_names.tsv` — Contains drug names and their unique SIDER identifiers.

2. **PathFX**

   [PathFX Drug Target Data](https://github.com/jenwilson521/PathFX/blob/master/rscs/Pfx050120_dint.pkl)

   * `Pfx050120_dint.pkl` — Pickled dictionary containing DrugBank drugs and their associated targets.

3. **DrugBank Vocabulary**

   [DrugBank Open Data](https://go.drugbank.com/releases/latest#open-data)

   * `drugbank_vocabulary.csv` — Contains common drug names and synonyms associated with DrugBank identifiers.

4. **DrugBank Release 5.1.6**

   [DrugBank Releases](https://go.drugbank.com/releases)

   * `Drugbank050120.xlsx` — Contains data from DrugBank release version 5.1.6 used to obtain ATC classifications.
   * The data was parsed following the approach described in [this notebook](https://github.com/dhimmel/drugbank/blob/gh-pages/parse.ipynb).

---

## Intermediate Data

The repository also contains several Excel files containing processed data and statistical results from the original study and our extensions.

### `Intermediate_Data/Characteristics.xlsx`

Contains:

* **Data characteristics** — Counts of side effects, associated drugs, DrugBank ID matches, and matrix matches.
* **LR vs. RFC** — Comparison of Logistic Regression and Random Forest Classifier predictions across 30 side effects using 100× bootstrap sampling with random undersampling of negative cases.
* **Average accuracy across feature combinations** — Model performance for:

  1. ATC
  2. DT
  3. DT/PathFX
  4. DT/ATC
  5. DT/PathFX/ATC
* **ANOVA-RM** — Repeated-measures ANOVA comparing the five feature combinations.

### `Intermediate_Data/LR_Coefficients.xlsx`

Contains Logistic Regression coefficient analyses, including:

* Coefficients for the 10 most common unapproved drug targets across 30 side effects.
* Top and bottom 30 coefficients for **gastrointestinal disorder**.
* Top and bottom 30 coefficients for **hypersensitivity**.
* Top and bottom 30 coefficients for **dermatitis**.

### `Intermediate_Data/all_ttest_results.xlsx`

Contains paired t-test results comparing model performance, including:

* **DT vs. DT/PathFX**
* **DT/ATC vs. DT/ATC/PathFX**
* **ATC vs. DT**
* **DT vs. DT/ATC**
* **DT/PathFX vs. DT/ATC/PathFX**

---

## Project Recognition

This project was conducted as part of **C&S BIO M185: Thesis Research Opportunities in Computational and Systems Biology** at the **University of California, Los Angeles (UCLA)**.

The project was subsequently submitted to the **2025–2026 UCLA Library Prize for Undergraduate Research**, where it received **2nd Place in Science, Technology, Engineering & Mathematics (STEM)**.

As part of the library prize, the project is now available as an open-access publication through eScholarship, the University of California's open-access publishing platform.

**[UCLA Library Prize / eScholarship Publication](SCHOLARSHIP_LINK_HERE)**

---

## Team

- Vyas Koduvayur
- Jenna Jabourian
- Melody Mao
- Flicka Zhang
- Abeni Liu

All team members contributed to **brainstorming, analysis, and writing**.

---

## Acknowledgements

We would like to thank **Dr. Brian Nadel** for his guidance and support throughout the development of this project in C&S BIO M185 at UCLA.

We also thank **Liu and Wilson** for providing the foundational study and computational framework on which this project was built.
