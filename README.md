# Bridge Condition Modelling for Infrastructure Asset Management

An applied regression and exploratory analytics project using Texas bridge data to identify the structural and operational factors most associated with bridge condition.

## Overview

This project analyses bridge-condition data to identify which characteristics are most strongly associated with overall structural condition and how well a multiple linear regression model can predict condition at network scale.

The workflow includes target construction, data preparation, exploratory analysis, regression modelling, residual diagnostics, and practical interpretation for infrastructure asset management.

## Problem Statement

Bridge owners need evidence on which characteristics are most useful for prioritising maintenance and monitoring deterioration across large infrastructure networks.

This project investigates whether bridge age, traffic volume, truck intensity, material, and design can explain meaningful variation in overall bridge condition, and whether a multiple linear regression model can provide a useful decision-support tool for asset management.

## Dataset

The project uses a Texas bridge dataset containing bridge characteristics and component condition ratings.

### Key variables

- `Deck_rating`
- `Superstr_rating`
- `Substr_rating`
- `Year`
- `AverageDaily`
- `Trucks_percent`
- `Material`
- `Design`

To create a single modelling target, deck, superstructure, and substructure ratings are treated as integer scores and summed into a continuous `Condition_score` ranging from 0 to 27. The final cleaned modelling dataset contains **33,821 bridges**. :contentReference[oaicite:0]{index=0}

## Project Pipeline

The overall workflow is:

- Load and inspect the raw bridge dataset
- Derive a continuous bridge condition target
- Engineer bridge age from construction year
- Simplify sparse material and design categories
- Review outliers and define the final modelling dataset
- Explore how condition varies with age, traffic, material, and design
- Fit a multiple linear regression model
- Evaluate model fit and inspect residuals
- Interpret findings for infrastructure asset management

## Data Preparation

Several preparation steps were used to make the analysis more robust and interpretable:

- derive `Age` from bridge year
- construct `Condition_score` from structural component ratings
- simplify sparse `Material` categories
- simplify sparse `Design` categories
- exclude very old bridges aged 100+ years
- retain extreme traffic values where they appeared plausible rather than obvious data errors

These steps produced a clean modelling dataset with complete predictors and target values. :contentReference[oaicite:1]{index=1}

## Exploratory Analysis

The exploratory analysis was used to identify which factors showed the clearest relationship with bridge condition before fitting the regression model.

### Main exploratory findings

- **Age** is the strongest single predictor of bridge condition.
- **Material** shows a meaningful relationship with condition.
- **Design** contributes some variation, but less strongly than age.
- **AverageDaily** and **Trucks_percent** show weak linear relationships with condition.

The notebook reports the following correlations with `Condition_score`:

- **Age:** `r = -0.590`
- **AverageDaily:** `r = 0.033`
- **Trucks_percent:** `r = -0.049` :contentReference[oaicite:2]{index=2}

## Regression Modelling

A multiple linear regression model is fitted using:

- `Age`
- `AverageDaily`
- `Trucks_percent`
- `Material_simplified`
- `Design_simplified`

The purpose of the model is not to produce perfect predictions, but to estimate how useful these structural and operational variables are for explaining overall bridge condition.

## Results

The final regression model achieved:

- **R² = 0.454**
- **RMSE = 1.468** :contentReference[oaicite:3]{index=3}

This indicates that the model explains a meaningful, but incomplete, share of variation in bridge condition. In practical terms, it is useful for network-level prioritisation and screening, but not as a replacement for engineering inspection.

## Key Findings

- Bridge **age** is the dominant predictor of lower condition.
- **Material** is the strongest secondary factor.
- **Design** has some influence, but less than age and material.
- Traffic variables are weaker predictors once the structural variables are considered jointly.
- A simple linear model provides useful decision-support value, but substantial variation remains unexplained.

## Asset-Management Implications

This project shows how a relatively simple statistical model can support infrastructure decision-making by:

- highlighting older bridges as higher-priority candidates for review
- treating material type as a meaningful maintenance-risk stratifier
- showing that traffic volume alone is not the main driver of bridge condition
- providing a scalable first-pass tool for prioritisation across a large network

The model is best interpreted as a **screening and triage tool**, not a substitute for detailed engineering assessment.

## Limitations

This project is intentionally careful about the scope of its conclusions.

- The model is linear and therefore does not capture every possible non-linear effect or interaction.
- Important omitted variables may include maintenance history, environment, inspection practice, and construction quality.
- `Condition_score` is a practical summary target, but not a complete engineering description of bridge health.
- The analysis is observational and predictive rather than causal.

## Future Improvements

Several extensions could improve the analysis:

- test non-linear or tree-based models
- include interaction terms
- incorporate environmental and maintenance variables
- compare regularised regression approaches
- evaluate out-of-sample performance more explicitly
- build a simple dashboard for maintenance prioritisation

## Tech Stack

- Python
- NumPy
- pandas
- matplotlib
- seaborn
- scikit-learn
- statsmodels
- Jupyter Notebook

## How to Run

1. Clone this repository.
2. Install dependencies from `requirements.txt`.
3. Ensure `texas_bridges.csv` is available inside the `data/` directory.
4. Open `notebooks/bridge_condition_modelling.ipynb`.
5. Run the notebook cells in order to reproduce data preparation, exploratory analysis, modelling, and evaluation.

## Repository Structure

```text
bridge-condition-modelling/
├── README.md
├── requirements.txt
├── data/
│   ├── README.md
│   └── texas_bridges.csv
├── notebooks/
│   └── bridge_condition_modelling.ipynb
├── .gitignore
└── LICENSE
