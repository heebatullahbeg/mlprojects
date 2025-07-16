# Project Overview
This project aims to predict cancer metastasis (spread of cancer to other organs) using genomic, clinical, and symptom data. The goal is to identify key predictors of metastasis and develop a model to assist clinicians in early intervention. The best-performing model achieved 64.2% accuracy using clinical and symptom features, with logistic regression as the optimal algorithm. Below is a detailed breakdown of the methodology, results, and insights.

## Dataset Overview
Source: [Esophagogastric Cancer (MSK, J Natl Cancer Inst 2023)](https://www.cbioportal.org/study/summary?id=egc_msk_2023)

#### Target Variable:

Metastatic/Non-Metastatic: Binary label derived from metastasis-related columns.

#### Features:

Genomic: Fraction Genome Altered, Mutation Count, MSI Score, TMB, etc.

Clinical: Age at Diagnosis, Sex, Cancer Type, Histology, etc.

Symptoms: Weight Loss, Abdominal Pain, Nausea/Vomiting, etc.

#### Preprocessing:

Encoded categorical variables (e.g., MSI Type mapped to ordinal values).

Removed columns with potential data leakage (e.g., Stage, direct metastasis indicators).

Imputed missing values (median for numeric, mode for categorical).

## Exploratory Data Analysis (EDA)
Key Findings:
Class Distribution:

Metastatic: 36%

Non-Metastatic: 64%

Metastatic Count

![image](https://github.com/user-attachments/assets/2f1f4e57-5255-421f-8471-109f68db3a3f)

Feature Correlations:

Correlation Matrix

![image](https://github.com/user-attachments/assets/ee50a924-3609-4a05-8de0-fe409774ea66)

Symptoms: Weight Loss (correlation = 0.24) and Abdominal Pain (0.19) showed the strongest positive correlation with metastasis.

Cancer Type Analysis:
Metastasis rates varied significantly by cancer type (e.g., pancreatic cancer had higher metastasis prevalence).

Age Distribution:
Metastatic patients were slightly older (median age: 62 vs. 58).

![image](https://github.com/user-attachments/assets/451edae5-9393-435c-9107-15c23e558a7c)

Genomic: Weak correlations (e.g., Mutation Count: 0.08, TMB: 0.05).

![image](https://github.com/user-attachments/assets/0febc32e-fd82-4ffc-9462-e680b199aa4a)


## Modeling Approach
Algorithms Tested:

Logistic Regression
Random Forest
XGBoost
SVM

Feature Groups Evaluated:
Genomic, Clinical, Symptoms, and combinations.

Methodology:
Train-Test Split: 75% training, 25% testing (stratified).

Preprocessing Pipeline:

Numeric features: Median imputation + standardization.

Categorical features: Mode imputation + one-hot encoding.

Evaluation Metrics: Accuracy, ROC-AUC, Precision-Recall.

## Results

#### Model Performance:
Model	Accuracy	ROC-AUC	Precision	Recall

Logistic Regression	62.8%	0.67	0.61	0.59

Random Forest	59.7%	0.63	0.58	0.53

XGBoost	57.5%	0.61	0.55	0.51

SVM	60.6%	0.65	0.59	0.55

![image](https://github.com/user-attachments/assets/fe61c9c7-5126-4692-bd27-d7311931229a)

## Key Visualizations:
Confusion Matrix (Logistic Regression):

![image](https://github.com/user-attachments/assets/2c8798b9-3d57-4d2d-96d9-6971f017aabf)

## Discussion

Reasons behind LR outperforming:
Linearity Assumption: The relationship between features and metastasis may be primarily linear.

Overfitting in Tree Models: Random Forest and XGBoost likely overfit due to limited data (~500 samples).

Class Imbalance: Logistic Regression handled imbalance better without explicit weighting.

Limitations:
Moderate Accuracy: A naive "always predict non-metastatic" baseline would achieve 64% accuracy, suggesting limited model utility.

Class Imbalance: Metastatic cases (36%) were underrepresented, affecting recall.

Feature Leakage Risk: Despite removing explicit metastasis columns, latent leakage (e.g., symptoms tied to late-stage cancer) may persist.

## Conclusion

This project demonstrates that clinical and symptom data are more predictive of metastasis than genomic markers in this dataset. While logistic regression achieved the best performance (64.2% accuracy with Clinical + Symptoms features). 

![image](https://github.com/user-attachments/assets/b7220c34-75ef-4635-b375-dd9246c61763)

Future work should prioritize addressing class imbalance and enriching genomic data to improve predictive power.
