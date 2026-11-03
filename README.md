# Molecular Solubility Prediction with Machine Learning

Predicting aqueous solubility from molecular descriptors using Linear Regression and Random Forest Regression.

## Project overview

Aqueous solubility matters in chemical research and early-stage drug discovery. This project uses the ESOL (Delaney) dataset to estimate `logS` (logarithmic aqueous solubility) from molecular descriptors. It compares a linear baseline with a nonlinear ensemble method.

**Tech stack:** Python · Pandas · NumPy · Scikit-learn · Matplotlib · Seaborn · Jupyter

## Dataset and features

The notebook loads a publicly hosted copy of the ESOL dataset (1,128 compounds) from [Data Professor's dataset repository](https://github.com/dataprofessor/data/blob/master/delaney_solubility_with_descriptors.csv). Its four predictors are:

- `MolLogP`: octanol–water partition coefficient estimate
- `MolWt`: molecular weight
- `NumRotatableBonds`: number of rotatable bonds
- `AromaticProportion`: proportion of aromatic atoms

**Target:** `logS`. The dataset is fetched at runtime; no dataset copy is bundled. Confirm original dataset attribution and usage terms before redistribution.

## Approach

1. Load and inspect the dataset.
2. Separate molecular descriptors from `logS`.
3. Split the records into 80% training and 20% testing (`random_state=42`).
4. Standardise inputs for Linear Regression using a scaler fitted only on the training set.
5. Fit Linear Regression and Random Forest Regression (`n_estimators=200`, `random_state=42`).
6. Evaluate held-out predictions with R², RMSE and MAE, and visualise predicted vs actual solubility.

## Results

Metrics recorded in the uploaded notebook's saved outputs (not independently rerun during packaging):

| Model | Test R² | Test RMSE | Test MAE |
| --- | ---: | ---: | ---: |
| Linear Regression | 0.7706 | 0.9995 | 0.7964 |
| Random Forest Regression | 0.8876 | 0.6997 | 0.5040 |

The Random Forest performed better on this held-out test split. RMSE and MAE are measured in logS units.

![Predicted versus actual logS for both models](images/model_predictions.png)

## How to run

1. Clone or download this repository.
2. Create a Python virtual environment (recommended).
3. Install dependencies:

   ```bash
   pip install -r requirements.txt
   ```

4. Launch `jupyter lab`, open `molecular_solubility_prediction.ipynb`, and run all cells from the top.

**Note:** The notebook requires an internet connection to fetch the CSV from GitHub. It no longer disables SSL certificate verification.

## Limitations and next steps

- This is a single random train/test split; repeated cross-validation and hyperparameter tuning would provide more reliable estimates.
- Results may vary across dependency versions and dataset updates.
- The four molecular descriptors are a limited representation of chemical structure.
- A stronger external validation approach could use scaffold- or time-based splitting rather than a random split.
- Consider feature importance, error analysis and additional regressors (e.g. gradient boosting).

## Files

- `molecular_solubility_prediction.ipynb` — analysis and saved outputs
- `images/model_predictions.png` — comparison chart extracted from the notebook
- `requirements.txt` — Python dependencies
- `.gitignore` — files excluded from version control

## References

- [Public ESOL dataset mirror (Data Professor)](https://github.com/dataprofessor/data/blob/master/delaney_solubility_with_descriptors.csv)
- Delaney, J. S. (2004). ESOL: Estimating Aqueous Solubility Directly from Molecular Structure. *Journal of Chemical Information and Computer Sciences*, 44(3), 1000–1005.
- Sheridan, R. P. (2013). Time-split cross-validation as a method for estimating the goodness of prospective prediction. *Journal of Chemical Information and Modeling*, 53(4), 783–790.

## Author

Nontokozo Dladla — MSc Data Science candidate, University of the Witwatersrand.
