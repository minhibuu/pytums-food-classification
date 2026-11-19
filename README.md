# PyTUMs — Food Classification with Machine Learning

Final group project for **Python and Advanced Data Science** at the **Technical University of Munich**, taught by Batuhan Can. Submitted on 21 July 2026.

The project predicts **NOVA food-processing groups** and **Nutri-Score grades** from Open Food Facts product information, and examines whether nutrient-based clusters align with these labels.

**Team** — Maximilian Seidlitz, Niklas Matusik, Bilal Mert, and Bui Ngoc Minh Quach.

This portfolio release is based on the submitted final notebook. The original collaborative repository is maintained under the team's GitHub account below.

[Original team repository](https://github.com/maxseidlitz/Nutrition_PythonAdvDataScience)

## Contributions

| Work | Contributors |
| --- | --- |
| Domain knowledge and hypotheses | Bilal Mert and Bui Ngoc Minh Quach |
| Data extraction, cleaning, feature preparation, and exploratory analysis | Bilal Mert and Bui Ngoc Minh Quach |
| Machine-learning preprocessing and clustering | Niklas Matusik and Maximilian Seidlitz |
| Classification models, model comparisons, tuning, and conclusion | Niklas Matusik and Maximilian Seidlitz |

The contribution table follows the submitted notebook.

## Analysis

[Open the complete notebook](PyTUMs_Final_Project.ipynb)

The workflow streams Open Food Facts through Hugging Face, draws a reservoir sample of 100,000 products with seed 42, and caches it locally. It constructs nutrient, ingredient-count, additive-count, and product-category features, applies plausibility filters, and creates separate datasets for NOVA and Nutri-Score.

The notebook includes exploratory plots, stratified train/test splits, imputation and encoding pipelines, K-means clustering with PCA visualization, six baseline NOVA classifiers, cross-validated hyperparameter searches, feature importance, and a nutrient-only comparison.

## Results reported in the submission

| Task | Best baseline model | Weighted F1 |
| --- | --- | --- |
| NOVA classification | Random Forest | 0.8573 |
| Nutri-Score classification | Random Forest | 0.8269 |

The submitted run used 23,406 products for NOVA and 28,924 for Nutri-Score. These figures describe the original cached sample. The published notebook has cleared outputs, and these results have not been regenerated during release preparation.

## Run locally

Python 3.13 was used in the supplied project environment. From the repository root, create an environment and start JupyterLab.

```bash
python3.13 -m venv .venv
source .venv/bin/activate
python -m pip install -r requirements.txt
jupyter lab
```

Open `PyTUMs_Final_Project.ipynb` and execute the cells in order. The scientific package versions come from the team project's requirements file. JupyterLab and the Python kernel are also included.

The notebook first looks for `openfoodfacts_raw_sample.parquet` in the repository root. If this cache is unavailable, it streams the public database and builds a reservoir sample across the full stream. This can take substantial time and bandwidth. The notebook writes the sample, sampling metadata, and two derived CSVs locally. These files are ignored by Git.

A smaller sample can be configured using `SAMPLE_SIZE` for exploration. It will change model results and may leave some classes too small for the configured splits or cross-validation. To use a different sample, move the existing cache aside first.

## Reproducibility and interpretation

The random seed is fixed at 42. The source database is continuously updated, and the notebook does not pin a dataset revision. Exact reproduction of the submission's results therefore requires its original cached sample. A new stream can yield different products and estimates even with the same seed.

NOVA labels in Open Food Facts can depend on ingredient and additive information, which overlaps with the predictors. The nutrient-only comparison investigates this overlap. Class imbalance, missing labels, and country coverage also affect interpretation. The notebook preserves the submission's written interpretations, which refer to its original sample.

Notebook format and Python cell syntax were checked during release preparation. The full streaming, model-fitting, and tuning workflow was not rerun.

## Data and attribution

The data source is Open Food Facts and its community contributors, accessed through the Hugging Face product database. Consult the provider's current data terms before redistributing a snapshot or derived database.

- [Open Food Facts data and reuse terms](https://world.openfoodfacts.org/data)
- [Open Food Facts product database on Hugging Face](https://huggingface.co/datasets/openfoodfacts/product-database)

The notebook retains the team's academic references. This release adds no blanket license to the group code.

## Release changes

Saved outputs and notebook metadata were cleared. The university SharePoint sharing link was removed. Data access now opens the remote stream only when the local raw-data cache is absent. The research and modeling procedures follow the submitted notebook.
