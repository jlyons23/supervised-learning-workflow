# Supervised Learning Workflow: Regression and Classification

A supervised learning workflow worked through on two contrasting problems. Supervised
learning splits by outcome type: regression for continuous outcomes and classification
for categorical ones. This project covers both, using a dataset suited to each. The
subject is the method: how to select, tune and honestly evaluate a
model and how to match the technique to the problem.

- **Regression** is about reducing a wide predictor space to the predictors
  that carry the signal.
- **Classification** is about comparing model families on one problem and
  finding which predicts best on unseen data.

Both are done in R and validated with cross-validation.

**Rendered report:** view it at <https://jlyons23.github.io/supervised-learning-workflow/> or open `index.html` locally.

## Regression: Predicting species richness

Predict `spnm` (species count at a site) from around 30 trait, soil and climate
predictors, with a small sample (n around 41). Too many predictors for the sample size,
so the task is reduction.

- Forward stepwise subset selection (`leaps`), subset size chosen by BIC, Cp and adjusted R2.
- Lasso shrinkage (`glmnet`), penalty chosen by cross-validation with the `lambda.1se` rule.
- Both validated with a leave-one-out cross-validation loop written by hand.
- A bootstrap 99% confidence interval (percentile method, coded manually) for the
  correlation between a chosen predictor and the response.

## Classification: Predicting in-hospital mortality

Predict a binary mortality `outcome` for ICU heart-failure patients from clinical
measurements (MIMIC-III derived data). The classes are imbalanced, with far more
survivors than deaths, and that is the crux of the interpretation.

- Stratified 60/40 train-test split.
- Four model families, each tuned on the training data by cross-validation then tested
  on the held-out set: a decision tree (CV-pruned), a random forest (`mtry` tuned via
  out-of-bag error), LDA (threshold tuned via CV) and kNN (k tuned via CV).

## Structure

```
supervised-learning-workflow/
├── README.md
├── report.Rmd        
├── index.html        
├── data/README.md
└── .gitignore
```

All analysis code is in `report.Rmd`.

## Reproducing

1. Install R and the packages: `MASS`, `tidyverse`, `leaps`, `glmnet`, `tree`,
   `randomForest`, `class`, `gt`, `patchwork`, `here`.
2. Download the two datasets (see `data/README.md`) into `data/`.
3. Render: `rmarkdown::render("report.Rmd")`.

## Notes and limitations

- The regression half tunes the model and then evaluates it with LOOCV on the same small sample,
  giving the cross-validated error a mild optimistic bias. This is a deliberate trade-off
  given the small sample size.
- The classification half imputes missing values by median across the full dataset before the split, which
  lets the test set influence the imputed values. It is negligible here but a stricter
  pipeline would fit the imputation on the training set alone.
- Both samples are small, so results illustrate the method rather than standing as
  definitive findings.

## Data

Two public Dryad datasets. See `data/README.md` for sources, citations and cleaning notes.
