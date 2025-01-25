### Project Overview

This project develops disease prediction system leveraging machine learning models to classify diseases based on patient symptoms, demographic data, and health risk factors.
There are several models are trained on a dataset containing patient profiles and their corresponding outcomes, with a focus on binary classification (Positive/Negative disease outcome).

## Objectives

1. Preprocess and clean the patient health dataset.
2. Evaluate the performance of various machine learning models for disease prediction.\
3. Identify the best-performing model and assess its interpretability and real-world applicability.

## Dataset Description

The dataset contains the following columns:

1. Age: Numeric
2. Gender: Categorical (Male/Female)
3. Fever, Cough, Fatigue, Difficulty Breathing: Binary (Yes/No).
4. Blood Pressure, Cholesterol Level: Categorical (Low/Normal/High).
5. Outcome Variable: Target variable (Positive/Negative disease outcome).

Risk Factor - a derived feature is created based on the patient's age, blood pressure, and cholesterol levels to enhance predictive performance.



## Data Preprocessing

![image](https://github.com/user-attachments/assets/636e4325-c59a-4b8d-948e-47dd8f06ea9a)

The above image represents the overall workflow of the project.

![image](https://github.com/user-attachments/assets/427c66fe-ef04-463b-a722-e7525b087c17)

_Before processing_

**Encoding Features**

1. Binary variables (e.g., Fever, Cough) were mapped to integers (Yes = 1, No = 0).
2. Categorical variables (e.g., Gender, Blood Pressure) were encoded using predefined mappings.
3. Target variable (Outcome Variable) was mapped to Positive = 1 and Negative = 0.

**Feature Scaling**

Numerical features (e.g., Age, Risk Factor) were standardized using StandardScaler.

![image](https://github.com/user-attachments/assets/67469c5b-7c1c-4a38-a6ac-a669c61355e2)

_After processing_

### Train-Test Split

Data was split into training (80%) and testing (20%) sets, with stratified sampling to preserve class distribution.

![image](https://github.com/user-attachments/assets/3291419e-aee3-40fd-abef-5cb0a69b44ec)

### Models Used

1. Logistic Regression
2. Random Forest Classifier
3. XGBoost Classifier
4. CatBoost Classifier
5. Hyperparameter Tuning

Grid search was performed to optimize hyperparameters for Random Forest, XGBoost, and CatBoost models. The best parameters were used to train the final models.
Best XGBoost parameters: {'learning_rate': 0.05, 'max_depth': 5, 'n_estimators': 300}
Best CatBoost parameters: {'depth': 10, 'iterations': 500, 'learning_rate': 0.01}

### Evaluation Metrics

For evaluation I used the following metrics:

1. Accuracy
2. Precision, Recall, F1-Score (via Classification Report)
3. Confusion Matrix
4. ROC-AUC Score

### Results

1. Logistic Regression has an accuracy of 0.63
2. Random Forest has an accuracy of 0.80
3. XGBoost has an accuracy of 0.73
4. CatBoost has an accuracy of 0.76

Best Model: Random Forest Classifier with an accuracy of 0.80.

![image](https://github.com/user-attachments/assets/61803290-7c53-4de1-a191-c77b11b77829)

![image](https://github.com/user-attachments/assets/37d9434d-8c2f-4893-8b66-c13e619d0897)


