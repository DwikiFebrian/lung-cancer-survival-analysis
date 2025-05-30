# lung-cancer-survival-analysis
📊 Survival analysis on lung cancer patients using R — includes Kaplan-Meier curves, Cox regression modeling, and comprehensive data preprocessing.

# Lung Cancer Survival Analysis

This project performs survival analysis on lung cancer patient data using R. The analysis includes data cleaning, imputation, exploratory analysis, Kaplan-Meier survival curves, and Cox proportional hazards modeling.

## Project Overview

The objective is to identify factors influencing survival time in lung cancer patients. The process involves:
- Data preprocessing and imputation
- Exploratory data analysis and visualization
- Kaplan-Meier survival curves
- Cox proportional hazards model

## Data Source

The dataset is from the **NCCTG (North Central Cancer Treatment Group)** lung cancer study, consisting of 228 patients and 11 variables.

## Variables

- `id`: Patient ID
- `time`: Survival time (in days)
- `status`: 1 = censored, 2 = dead
- `age`: Patient’s age (years)
- `sex`: 1 = male, 2 = female
- `ph.ecog`: ECOG performance score
- `ph.karno`: Physician-assessed Karnofsky score
- `pat.karno`: Patient-assessed Karnofsky score
- `meal.cal`: Caloric intake during meals
- `wt.loss`: Weight loss in the last 6 months

## Methodology

### Data Preparation

1. **Missing Values**:
   - `meal.cal`: Imputed using regression
   - `wt.loss`: Imputed using median
   - Remaining NA rows dropped

2. **Outlier Handling**:
   - Removed using the IQR method for numeric features

3. **Feature Engineering**:
   - Categorization:
     - `age_cat`: Young / Middle / Old
     - `ph.karno_cat`, `pat.karno_cat`: Low / Medium / High
     - `meal.cal_cat`: Low / Medium / High
     - `wt.loss_cat`: Gain/Stable / MildLoss / SevereLoss
   - One-hot encoding applied to categorical features

### Survival Analysis

1. **Kaplan-Meier Survival Curves**:
   - Stratified by: sex, age group, Karnofsky scores, calorie intake, and weight loss

2. **Cox Proportional Hazards Model**:
   - Multivariable model built using encoded categorical predictors
   - Hazard ratios and significance tested

## Key Findings

### ✅ Significant Predictors:
- **Sex**: Male patients have significantly higher risk (p = 0.0075)
- **Patient-assessed Karnofsky Score**: Low scores significantly increase hazard (p = 0.0063)

### ⚠️ Marginally Significant:
- **Old Age**: Shows a tendency for increased risk (p = 0.099)

### ❌ Non-Significant Predictors:
- Physician-assessed Karnofsky score
- Meal calorie intake
- Weight loss

## Visualization

Includes survival plots for:
- Sex
- Age groups
- Physician vs. patient Karnofsky scores
- Calorie intake groups
- Weight loss categories

## Requirements

### R Libraries
- `tidyverse`
- `survival`
- `survminer`
- `ggplot2`
- `broom`
- `fastDummies`

## Usage

1. Clone this repository
2. Place the dataset at: `/kaggle/input/ncctg-lung-cancer-data/cancer.csv`
3. Run the R script sequentially to reproduce results

## Model Output

- **Concordance index**: 0.648
- **Likelihood ratio test**: p = 0.002
- **Wald test**: p = 0.001
- **Log-rank (Score) test**: p = 0.0007

## Conclusion

Sex and patient’s own functional assessment are the strongest predictors of survival time. Age may play a role, while physician assessment and nutrition-related factors did not significantly impact outcomes in this dataset.

## License

For educational use only. Dataset credit to NCCTG lung cancer study.
