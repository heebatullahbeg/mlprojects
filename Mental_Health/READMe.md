# Predicting Social Anxiety and Work Interest: Mental Health Data Analysis

## Introduction

Mental health is a critical component of overall well-being. This project aims to predict key mental health outcomes, such as "Social Weakness" and "Work Interest," using a dataset on mental health attributes. Predicting these outcomes helps identify individuals who may require support in managing social anxiety or maintaining workplace engagement.
The dataset includes diverse features such as demographic data, employment history, and responses to mental health-related questions. Two machine learning models, Random Forest and XGBoost, are utilized to train and evaluate the predictive capabilities of these features.

## Data Preprocessing

The following steps were undertaken for data cleaning and preparation:

1. Dropped Irrelevant Columns: Columns such as "Timestamp" were removed as they were not relevant to the analysis.
2. Handled Missing Values: Missing values were replaced with "Nan," and observations with uninformative entries (e.g., "self_employed" = Nan) were excluded.
3. Categorical Encoding: Binary features like "self_employed" and "family_history" were encoded into 0 (No) and 1 (Yes). Ordinal fields, such as "Mood_Swings," were mapped to numerical values (e.g., Low = 0, Medium = 1, High = 2).
4. One-Hot Encoding: Non-ordinal categorical features (e.g., "Gender" and "Occupation") were transformed into dummy variables.
5. Target Variable: "Social Weakness" and "Work Interest" were used as target variables for model training and evaluation in separate iterations.

## Exploratory Data Analysis (EDA)

**Correlation Matrix**

![image](https://github.com/user-attachments/assets/e10d614a-86f7-4f23-a3aa-e08f0ac1d5e5)

A correlation heatmap was generated to visualize relationships between features. As seen in the heatmap:
"Family History" and "Treatment" exhibit a moderate positive correlation (0.37), highlighting the influence of family history on treatment-seeking behavior.
Features like "Growing Stress" and "Changes Habits" show weak correlations with the target variables but remain important for prediction.

## Feature Importance

The top 10 important features identified by the Random Forest model include:
1. Growing Stress
2. Changes Habits
3. Mental Health History
4. Mood Swings
5. Days Indoors
6. Coping Struggles
7. Gender (encoded)
8. Work Interest
9. Family History
10. Treatment

These insights provide a solid foundation for predictive modeling.

## Model Training and Evaluation

Two classifiers were trained and evaluated: Random Forest and XGBoost.

### Random Forest Results

![image](https://github.com/user-attachments/assets/81843841-8ee2-456e-83bd-a49b459342f8)

_Target Variable: Social Weakness_

![image](https://github.com/user-attachments/assets/70fc819b-cdd6-4545-8406-0b87a768fab0)


_Target Variable: Work Interest_

1. Accuracy: 98%
2. Precision, Recall, and F1-Score:
3. Class 0 (Low Interest): Precision = 0.98, Recall = 0.98, F1-Score = 0.98
4. Class 1 (Medium Interest): Precision = 1.00, Recall = 1.00, F1-Score = 1.00
5. Class 2 (High Interest): Precision = 0.97, Recall = 0.98, F1-Score = 0.98

### XGBoost Results

![image](https://github.com/user-attachments/assets/78af325c-a631-47bf-8195-f8c1195fbeeb)

_Target Variable: Social Weakness_


![image](https://github.com/user-attachments/assets/d48ea630-9224-4860-af31-c74b7c6265d8)

_Target Variable: Work Interest_

For Social Weakness as target variable:

1. Accuracy: 99%
2. Precision, Recall, and F1-Score:
3. Class 0 (Low Interest): Precision = 0.99, Recall = 0.98, F1-Score = 0.98
4. Class 1 (Medium Interest): Precision = 1.00, Recall = 1.00, F1-Score = 1.00
5. Class 2 (High Interest): Precision = 0.98, Recall = 0.98, F1-Score = 0.98

For Work Interest as target variable:

1. Accuracy: 99%
2. Precision, Recall, and F1-Score:
3. Class 0 (Low Interest): Precision = 0.99, Recall = 0.98, F1-Score = 0.98
4. Class 1 (Medium Interest): Precision = 1.00, Recall = 1.00, F1-Score = 1.00
5. Class 2 (High Interest): Precision = 0.98, Recall = 0.98, F1-Score = 0.98

The XGBoost classifier slightly outperformed Random Forest, achieving a 99% accuracy. Both models demonstrated excellent performance in predicting all classes for both Social Anxiety and Work Interest which are metrics corporates and companies will be interested in.
Evaluation metrics for this target variable were similarly impressive, with both classifiers achieving high precision, recall, and F1-scores.

**Confusion Matrices**


![image](https://github.com/user-attachments/assets/776c730f-0103-49b1-8f5e-1ec1f58e5aef)

_Target Variable: Social Weakness_


![image](https://github.com/user-attachments/assets/1ffaae4a-437c-413d-92df-940aadb27fd5)

_Target Variable: Work Interest_

Heatmaps of confusion matrices for both classifiers revealed minimal misclassifications, indicating robust model performance.

## Conclusion

This project successfully predicted mental health outcomes such as "Work Interest" and "Social Weakness" with high accuracy using Random Forest and XGBoost classifiers. Key insights include:
Features such as "Growing Stress," "Changes Habits," and "Mental Health History" play a critical role in predictions.
The XGBoost model consistently outperformed Random Forest, though the difference was marginal.

**Enhancements**

1. Incorporating additional datasets to improve generalizability.
2. Exploring causal relationships between features and mental health outcomes.
3. Implementing real-time prediction systems for workplace mental health monitoring.
