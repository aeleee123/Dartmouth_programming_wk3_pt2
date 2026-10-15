# Dartmouth_programming_wk3_pt2
Data Selection and Final Project Planning Lab

Cirrhosis Patient Survival Prediction
Project Overview
This project explores demographic, clinical, and laboratory variables associated with death observed during follow-up among patients with primary biliary cirrhosis. The initial notebook examines dataset suitability, structure, missingness, and candidate preprocessing steps. A future machine learning pipeline will evaluate binary classification models.
Important: The proposed binary outcome represents observed death status, not confirmed survival or a fixed-time mortality probability. Censored observations do not establish that a patient survived beyond their last follow-up.
Data Source
- Dataset: Cirrhosis Patient Survival Prediction
- Provider: UCI Machine Learning Repository
- URL: https://archive.ics.uci.edu/dataset/878/cirrhosis+patient+survival+prediction+dataset-1
- Observations: 418 patients
- Original status categories: D (death), C (censored), CL (censored due to liver transplantation)
The inspected working dataframe contains 418 rows and the derived column Death_Outcome.
Research Question
Can demographic, clinical, and laboratory variables help classify whether death was observed during follow-up among patients with primary biliary cirrhosis?
Proposed Binary Outcome
Original Status	Derived Death_Outcome	Interpretation
D	1	Death observed during follow-up
C	0	Death not observed before censoring
CL	0	Death not observed before liver transplantation


The original Status variable should be retained for transparency. The binary mapping is a simplification for the classification assignment and should not be interpreted as a standard survival-analysis endpoint.
Exploratory Data Assessment
The following missing-value counts were observed in the 418-row working dataset:
Variable	Missing	Missing (%)
Drug	106	25.4
Ascites	106	25.4
Hepatomegaly	106	25.4
Spiders	106	25.4
Cholesterol	134	32.1
Copper	108	25.8
Alk_Phos	106	25.4
SGOT	106	25.4
Tryglicerides	136	32.5
Platelets	11	2.6
Prothrombin	2	0.5
Stage	6	1.4


No missing values were reported for ID, N_Days, Status, Age, Sex, Edema, Bilirubin, Albumin, or the derived Death_Outcome.
Several variables have exactly 106 missing observations; whether these are the same patients and why these values are absent require further investigation. Missingness should not be assumed to be random.
Planned Preprocessing
1. Verify data types, permissible categories, duplicates, and clinically implausible values.
2. Convert Age from days to years (divide by 365.25 once).
3. Retain ID as an identifier but exclude it from modeling.
4. Exclude N_Days from baseline predictors because it contains follow-up information unavailable at the intended prediction time. Exclude original Status as it directly defines the target.
5. Create Death_Outcome from Status as defined above.
6. Split into training and held-out test sets, stratifying by outcome where feasible.
7. Fit numeric imputation (candidate: median), categorical imputation, encoding, and any required scaling only on training data, using a pipeline to avoid leakage.
8. Explore missingness patterns and perform sensitivity analyses for variables with substantial missing data.
The precise final predictor set and preprocessing choices will be determined after data exploration.
Proposed Modeling and Evaluation
The final project will compare suitable binary classification methods, potentially including logistic regression and tree-based models. Candidate metrics are:
- Primary: ROC-AUC (discrimination across thresholds)
- Secondary: recall/sensitivity, precision, F1-score, and confusion matrix
Stratified cross-validation within the training set is planned, with final evaluation on held-out data. No model performance results are reported at this stage.
Key Limitations
- Censoring and liver transplantation are not equivalent to confirmed survival.
- Follow-up durations differ; a binary classifier of observed death does not estimate mortality risk at a standardized time horizon.
- Liver transplantation may be a competing event for death without transplant.
- Small sample size and substantial, potentially systematic missingness may limit model stability and generalizability.
- Any predictive associations are not evidence of causality or clinical readiness.
A time-to-event or competing-risks analysis would be more appropriate for estimating time-specific survival probabilities in a subsequent study.
Reproducibility
Suggested environment: Python 3 with pandas, NumPy, Matplotlib, Seaborn, and scikit-learn, run in Jupyter Notebook or Google Colab. Package versions and a runnable notebook should be recorded before final submission.
1. Obtain the dataset from the UCI URL above and follow its usage and attribution requirements.
2. Open the project notebook in Jupyter or Google Colab.
3. Update the dataset-loading path as needed, or use a notebook file-upload cell.
4. Run cells in order from a fresh runtime.
5. Verify that the dataframe contains 418 observations before any intentional row exclusions.
6. Use fixed random seeds for reproducible train/test splits and cross-validation.
Project status: Dataset selection, outcome planning, exploratory visualization, and missing-value assessment are in progress/completed as described in the assignment discussion; the final trained and evaluated predictive pipeline has not yet been documented here.
Data Citation
UCI Machine Learning Repository. Cirrhosis Patient Survival Prediction dataset. https://archive.ics.uci.edu/dataset/878/cirrhosis+patient+survival+prediction+dataset-1
