# World Happiness Report: Trend Analysis & Predictive Modeling

Analysis of the [World Happiness Report](https://worldhappiness.report/) (2015–2019), exploring what drives national happiness and predicting country happiness rankings with machine learning.

## Overview

The World Happiness Report ranks countries by self-reported citizen happiness and is widely used by governments and organizations to inform policy. This project:

- Reconciles five years of inconsistently-formatted survey data (each year uses different column names and country coverage) into a single clean dataset
- Explores trends in happiness scores over time, by country, and by region
- Identifies which socioeconomic features most strongly correlate with happiness
- Trains and compares three regression models — Linear Regression, KNN, and Random Forest — to predict 2019 happiness rankings from 2015–2018 data

## Key Findings

| Model | R² | MSE |
|---|---|---|
| **Linear Regression** | **0.73** | **542** |
| KNN (k=4) | 0.71 | 585 |
| Random Forest | 0.68 | 636 |

- Linear Regression outperformed the more complex Random Forest model, suggesting the relationship between happiness drivers and rank is largely linear at this sample size (~470 country-year rows)
- **GDP per capita** and **healthy life expectancy** are the strongest predictors of happiness — confirmed independently through correlation analysis, year-by-year breakdowns, and Random Forest feature importances
- Regional rankings are highly stable year over year: Australia/New Zealand, North America, and Western Europe consistently rank highest; Sub-Saharan Africa and Southern Asia consistently rank lowest

## Data

Yearly happiness survey data (2015–2019) sourced from the World Happiness Report, covering 150+ countries. 2015–2018 is used as the training set; 2019 is held out as the test set. Field definitions: [World Happiness Report FAQ](https://worldhappiness.report/faq/).

## Methodology

1. **Data cleaning & reconciliation** — standardized column names, country name spelling, and merged five years of data with differing schemas; imputed the small number of remaining missing values
2. **Exploratory data analysis** — central tendency trends, rank stability/improvement by country, correlation heatmaps (overall and by year), regional comparisons
3. **Modeling** — trained Linear Regression, KNN (tuned via elbow method), and Random Forest (tuned via `RandomizedSearchCV` + `GridSearchCV`) to predict 2019 happiness rank; compared performance via R², MSE, and squared-difference median
4. **Feature importance** — validated correlation-based findings against the Random Forest's built-in feature importances

## Tech Stack

Python · pandas · NumPy · scikit-learn · matplotlib · seaborn

## Repository Contents

- `World_Happiness_Analysis.ipynb` — full analysis notebook
- `2015.csv` – `2019.csv` — source data (World Happiness Report)

## Limitations & Next Steps

- Test set is a single year (2019); cross-validating across multiple year splits would give a more robust performance estimate
- Country name reconciliation was done manually — a fuzzy-matching approach would scale better
- `Dystopia Residual` is unavailable for 2018–2019, limiting its use as a training feature

## Author

Wilson Lin — partial data cleaning, correlation analysis, and data modeling.
Originally completed as a team project (CSE 351, Stony Brook University) with Ayden Budhoo.
