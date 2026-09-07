# Data

The datasets are not committed to this repository. Both are public domain (CC0) and
available from Dryad. Download them into this folder to run the analysis; the rendered
results are in `index.html` at the repository root, so the data is not needed just to
read the findings.

## Species richness (regression)

- **File:** `Weil_2021.csv` (41 rows, 30 columns)
- **Source:** https://doi.org/10.5061/dryad.cjsxksn63
- **Response:** `spnm`, total number of species present at a site.
- **Cleaning:** none. The analysis uses the raw Dryad file unmodified.

## In-hospital mortality (classification)

- **File:** `Zhou_2021_mortality.csv` (1176 rows, 43 columns)
- **Source:** https://doi.org/10.5061/dryad.0p2ngf1zd
- **Response:** `outcome`, 0 if the patient survived and 1 if they died.
- **Cleaning:** the analysis uses a reduced version of the raw Dryad file (which has 1177
  rows and 51 columns). Eight columns with high proportions of missing data were removed:
  `BMI`, `Neutrophils`, `Basophils`, `Lymphocyte`, `Creatine kinase`, `PH`,
  `Lactic acid`, `PCO2`, along with one row. To reproduce the input from the raw download,
  remove those eight columns. Some missing values remain in the retained columns and are
  handled in the analysis.
