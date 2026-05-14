# COVID-19 Risk Prediction: Pre-Existing Conditions and Severe Outcomes

## Project Overview

This project analyzes how demographic factors, health behaviors, and pre-existing medical conditions are associated with severe COVID-19 outcomes. The goal was to identify high-risk patient profiles and compare interpretable and nonlinear classification models for predicting adverse outcomes.

The project uses a translated Kaggle version of Mexico’s national COVID-19 surveillance dataset. The analysis focuses on laboratory-confirmed positive COVID-19 cases and evaluates whether patient characteristics can help predict severe outcomes.

## Research Questions

1. Which demographic factors, health behaviors, and pre-existing conditions are most strongly associated with severe COVID-19 outcomes across age groups?
2. Which combinations of pre-existing conditions and tobacco use are associated with elevated severe outcome risk, and how do these patterns vary by age group?
3. How do logistic regression and random forest models compare in predicting severe COVID-19 outcomes?

## Dataset

**Source:** Kaggle COVID-19 dataset derived from Mexico’s national COVID-19 surveillance data  
**Original size:** Approximately 1,048,575 observations  
**Final analytic dataset:** 388,719 confirmed positive COVID-19 cases  
**Original variables:** 21  
**Final cleaned variables:** 14  
**Reduced modeling dataset:** 8 variables after removing near-zero variance predictors  

### Target Variable

The target variable, `Adverse_Outcome`, was defined as a composite binary outcome:

- ICU admission
- Intubation
- Death

A patient was labeled as having an adverse outcome if they experienced at least one of these outcomes.

## Features Used

### Demographic Variables

- Age
- Age group
- Sex

### Health Behavior Variable

- Tobacco use

### Pre-Existing Conditions

- Diabetes
- Hypertension
- Obesity
- COPD
- Asthma
- Immunosuppression
- Cardiovascular disease
- Chronic renal disease
- Other disease

### Engineered Features

- `Condition_Count`: Total number of recorded pre-existing conditions
- `Age_Group`: Grouped age categories
- `Adverse_Outcome`: Composite severe outcome variable

## Methods

This project combined exploratory analysis, association rule mining, and supervised machine learning.

### Exploratory Data Analysis

EDA was used to examine:

- Outcome distribution
- Adverse outcome rates by sex
- Age distributions
- Hospitalization patterns by age group
- Condition prevalence
- Adverse outcome rates by condition
- Correlations among predictors and outcome variables

### Association Rule Mining

Association rule mining was used as an exploratory technique to identify combinations of risk factors associated with adverse outcomes.

Rules were evaluated using:

- **Support:** How often the condition-outcome pattern appeared
- **Confidence:** Probability of adverse outcome given the rule conditions
- **Lift:** How much higher the risk was compared with the baseline adverse outcome rate

Association rule mining helped identify repeated high-risk patterns involving:

- Older age groups
- Chronic renal disease
- Diabetes
- Hypertension
- Male sex
- Tobacco use in specific age groups

### Supervised Models

Two main classification approaches were compared:

1. **Logistic Regression**
   - Used for interpretability
   - Tested with and without interaction terms
   - Tested on full and reduced feature sets

2. **Random Forest**
   - Used for nonlinear modeling
   - Tested on full and reduced feature sets
   - Tuned using grid search and out-of-bag error

## Model Evaluation Metrics

Because the target class was imbalanced, accuracy alone was not treated as the main evaluation metric.

The models were evaluated using:

- Accuracy
- Sensitivity
- Specificity
- Precision
- F1-score
- ROC AUC

Sensitivity and F1-score were emphasized because the main modeling goal was to detect adverse outcome cases.

## Key Results

### Logistic Regression

The best logistic regression model used the full dataset with interaction effects.

| Metric | Result |
|---|---:|
| Accuracy | 85.2% |
| Sensitivity | 21.3% |
| Specificity | 96.9% |
| F1-score | 0.308 |
| AUC | 0.831 |

Logistic regression had strong specificity and interpretability, but it struggled to identify adverse outcome cases.

### Random Forest

The tuned full random forest model performed better at detecting adverse outcomes.

| Metric | Result |
|---|---:|
| Accuracy | 82.0% |
| Sensitivity | 55.7% |
| Specificity | 86.8% |
| F1-score | 0.488 |
| AUC | 0.825 |

Random forest had slightly lower accuracy and specificity than logistic regression, but it substantially improved sensitivity and F1-score.

## Main Findings

- Age was the strongest predictor of adverse COVID-19 outcomes.
- Risk increased as the number of pre-existing conditions increased.
- Chronic renal disease was one of the most important high-risk conditions.
- Diabetes and hypertension were consistently associated with elevated risk.
- Male patients had higher estimated odds of adverse outcome than female patients.
- Random forest provided the best balance between detecting adverse outcomes and controlling false positives.
- Logistic regression remained useful for interpretation but had limited sensitivity.

## Interpretation

The project showed a clear tradeoff between interpretability and predictive performance.

Logistic regression provided interpretable odds ratios, making it useful for explaining relationships between predictors and outcomes. However, its low sensitivity made it less effective for identifying severe cases.

Random forest better captured nonlinear relationships and interaction patterns, improving detection of the minority class. However, it was less interpretable and required variable importance analysis to explain results.

## Limitations

Several limitations should be considered:

- The dataset includes confirmed positive cases from medical units, so it may not represent all COVID-19 infections.
- The data comes from the first year of the pandemic, before widespread vaccination and later variants.
- The dataset does not include lab values, oxygen saturation, vaccination status, symptoms, or detailed clinical measures.
- Some conditions may have been self-reported or underreported.
- Patients initially sent home may have later experienced worsening outcomes.
- The model should not be used for clinical decision-making without further validation.

## Tools and Technologies

- R
- R Markdown
- Logistic Regression
- Random Forest
- Association Rule Mining
- Data Cleaning
- Feature Engineering
- Exploratory Data Analysis
- Model Evaluation
- ROC/AUC Analysis
- Imbalanced Classification
