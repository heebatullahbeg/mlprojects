# Diabetes Prediction Project

This project focuses on predicting diabetes using machine learning techniques on the Pima Indians Diabetes Dataset.
The goal is to develop and compare multiple classification models to predict diabetes onset based on various medical predictors.

### Dataset
The dataset contains information on 768 women from Pima population near Phoenix, Arizona, USA.
The tests were positive (1: diabetic) for 258 women and negative (0: non-diabetic) for 500.
The dataset has over Source: UCI Machine Learning Repository - Pima Indians Diabetes Database.
A few comments on the dataset:
The data is imbalanced and biased towards young people. Although I tried using SMOTE to rectify data imbalance, but the results were as promising as expected.

Features: The dataset contains 8 features:

![image](https://github.com/user-attachments/assets/dc871795-1c94-4ff9-8048-427a28ff7401)

![image](https://github.com/user-attachments/assets/4ca2ba64-a206-476a-8b29-6c06a7222955)

Target Variable: Diabetes Outcome (0: No Diabetes, 1: Diabetes)

### Block diagram of the project

![image](https://github.com/user-attachments/assets/fed4c0d4-9047-4259-b773-6d6b106e44f8)

### Data Loading and Exploratory Data Analysis
Used Pandas to load the dataset

1. Checked for missing values
2. Analyzed feature distributions
3. Created visualizations:

#### **Box plots**

![image](https://github.com/user-attachments/assets/1cd204bf-ae2e-4aa5-970b-eb55a0ed3c50)

There are quite a few outliers in the data - for instance, a regular patient wouldn't have 15 pregnancies or Blood Pressure = 0 or Glucose or BMI = 0 and so on.
Box Plot: The central rectangle represents the 25th to 75th percentile (e.g., the Interquartile range for Glucose is 100-145 the lines extending from this rectangle (Whiskers) represent the range of 1.5IQR values. The overall range of values for Glucose is between 50-200 THe circle on the graph (Outliers) can be seen in the case of Pregnancies where there are a couple above 15 (which is most likely an error)
As for the central line in each rectangle, that's is the median, e.g., the median age from the dataset is ~30

Box plots are great when comparing distributions of many sets of values. However, they are not ideal in case of Bimodal distributions, e.g., in case the data is clustered - lumped across different levels and not the regular Gaussian or Normal distributions (values clustered around the median). A good alternative might be frequency heatmaps.

#### **Correlation heatmap**

![image](https://github.com/user-attachments/assets/a2e05748-cb1c-47cd-bbe9-8a66543b2a27)

The correlation heatmap matrix (built on the Pearson correlation coefficient) helps understand the relation between different features:
Glucose and BloodPressure have a positive correlation (0.15) - as the glucose increases, the patient's blood pressure tends to increase as well. Insulin and glucose also have a positive correlation (0.32), and both these cases represent a weak to moderate correlation. Skin thickness and insulin, age and pregnancies have a strong positive correlation
Pregnancies and insulin have a negative correlation (-0.08) -> Insulin dips when a person has been through more pregnancies. Similarly, age and skin thickness have a (-0.11) correlation. The map is particularly important in case of Feature Selection (there might be overlap in information when choosing strongly correlated features, e.g., insulin and skin thickness)

#### **Pair plots**

![image](https://github.com/user-attachments/assets/f2a70749-d2ea-469f-80a7-5e16e71663cd)

the diagonal plots are density plots representing the distribution of each kernel.
Off-diagonal plots are scatter plots with regression lines showing the relation between two features.
Ex: Age and BMI have a negative correlation when the patient is diabetic, whereas a weak positive is in the case of a non-diabetic person. BMI and Skin Thickness have a positive relation regardless of whether the person is diabetic or non-diabetic.

#### **Histograms**

![image](https://github.com/user-attachments/assets/84b07407-f824-41c2-aebb-34da1af6aed7)

If we observe the graphs, we can infer:

10-15 pregnancies are not the norm, in fact they are pretty rare (might be errors)
The same goes for 0 blood pressure or glucose, which again isn't normal, so it can be an error.

### Data Preprocessing

1. Missing value handling
2. Feature scaling (StandardScaler)
3. Logarithmic transformation of skewed features
4. Renaming columns for consistency

### Techniques

## 1. K-Nearest Neighbors (KNN)

Distance-based classification
Hyperparameter tuning for optimal K

![image](https://github.com/user-attachments/assets/5b9b3527-53fb-4a5a-9585-d38719cc38db)

For k = 10, the model has the highest testing score, which means we can use this to create our model.

## 2. Decision Tree Classifier

Non-linear decision boundaries
Feature importance analysis

## 3. Logistic Regression

Probabilistic binary classification
Linear decision boundary

## 4. Logistic Regression with SMOTE (Synthetic Minority Over-sampling Technique)

Addresses class imbalance
Generates synthetic minority class samples

Based on the results, KNN outperformed Logistic regression and Decision Tree Classifiers in terms of Accuracy and predicting whether a patient has diabetes or not
1. KNN and Logistic Regression showed most consistent performance
2. SMOTE slightly improved class balance
3. Feature importance varies across models

### Feature Importance

![image](https://github.com/user-attachments/assets/a1199fe4-cc59-4ffa-bac4-f1a5fe203cad)

![image](https://github.com/user-attachments/assets/1968319f-fc97-406f-8f2b-2d88301016e2)

1. Glucose levels consistently significant
2. BMI and age show moderate predictive power
3. Genetic predisposition (Diabetes Pedigree Function) varies by model

### Detailed Model Analysis

#### K-Nearest Neighbors (KNN)

**Strengths**

Highest overall accuracy (80%)
Simple and intuitive algorithm
No assumptions about data distribution
Effective for non-linear relationships

**Limitations**

Computationally expensive for large datasets
Sensitive to feature scaling
Lower recall indicates missed diabetes cases
Performance depends on k-value selection

#### Decision Tree Classifier

**Strengths**

Highly interpretable model
Can capture non-linear relationships
Natural feature importance ranking
Handles both numerical and categorical data

**Limitations**

Lowest accuracy (72%)
Prone to overfitting
Unstable with small data variations
Less robust compared to ensemble methods

#### Logistic Regression Without SMOTE

Good baseline linear model
Probabilistic predictions
Moderate accuracy (78%)
Less complex than non-linear models

#### With SMOTE

Improved class balance
Slightly reduced accuracy
More robust minority class prediction
Demonstrates the importance of balanced training

### Comparative Performance Analysis

![image](https://github.com/user-attachments/assets/58ed4729-abca-4f08-9c9c-1f1c612417c4)

#### **Accuracy Comparison**

KNN: Best overall accuracy

**Precision and Recall Trade-offs**

1. KNN: High precision, low recall
2. Decision Tree: Balanced but lower precision
3. Logistic Regression: Moderate performance

### Limitations

1. Limited dataset size
2. Potential feature interaction complexity
3. Binary classification constraint

## Future Enhancements

1. Collect more diverse patient data
2. Implement advanced ensemble methods
3. Explore deep learning approaches
4. Develop more sophisticated feature engineering

## Ethical Considerations

1. Patient data privacy
2. Algorithmic bias
3. Transparent model interpretation
4. The project is a medical decision support system and not a replacement

