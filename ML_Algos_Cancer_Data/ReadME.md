# Comparative Analysis of Machine Learning Algorithms for Predicting Cancer Clinical Outcomes

## 1. Executive Summary
This project implements and compares three machine learning models (LightGBM, Random Forest, and Deep Neural Network) for predicting critical cancer outcomes using clinical and genomic data. The analysis focuses on three key prediction tasks: disease progression, treatment response, and immunotherapy effectiveness, achieving test accuracies up to 97.1% and ROC-AUC scores up to 0.987.
The dataset used from cBioPortal - Metastatic Esophagogastric Data. The feature correlation map can be seen as below:

![image](https://github.com/user-attachments/assets/492efa42-9057-4c60-8abd-b416c762cd29)

## 2. Methodology Overview
#### 2.1 Data Pipeline Architecture

![cancer_project](https://github.com/user-attachments/assets/6f6edb80-48ba-493f-940d-fb7b8f629f85)

#### 2.2 Key Components
Data Validation

11 essential features validated including:

Clinical: Age at Diagnosis, ECOG status

Genomic: Fraction Genome Altered, Mutation Count

Metastasis indicators

Strict column existence checking

Feature Engineering

Target Variables:

Disease Progression: High risk + deceased

Treatment Response: Low risk + long survival + alive

Immunotherapy Effectiveness: EBV+ + long survival

Preprocessing

Missing value handling with Iterative Imputer (MICE)

SMOTE for class balancing (train set only)

StandardScaler for feature normalization

## 3. Model Configuration

#### 3.1 Algorithm Specifications

Model	Parameters	Rationale

LightGBM - Parameters: learning_rate=0.01, n_estimators=200, max_depth=4;	Rationale: Conservative boosting for medical data

Working Principle:

Builds decision trees sequentially, correcting previous errors

Uses leaf-wise growth with depth limitation

Implements Gradient-based One-Side Sampling (GOSS)

Advantages:

Handles large datasets efficiently (30% faster than XGBoost)

Automatic categorical feature handling

Robust to missing values

Native support for class imbalance

Disadvantages:

Sensitive to hyperparameters

Potential overfitting with small datasets

Less interpretable than single trees

Clinical Rationale:

Ideal for structured medical data with mixed feature types and moderate sample sizes (n=500-10,000)

Random Forest - Parameters: n_estimators=200, max_depth=10;	Rationale: Deep trees for complex interactions

Working Principle:

Builds multiple decorrelated decision trees

Aggregates predictions through majority voting

Uses bootstrap sampling and feature randomization

Advantages:

Handles high dimensionality well

Built-in feature importance

Robust to outliers

Parallelizable training

Disadvantages:

Tendency to overfit noisy data

Memory intensive

Poor extrapolation beyond training range

Clinical Rationale:

Provides interpretable feature importance critical for medical decision-making

DNN - Parameters: hidden_layers=(64,32), max_iter=200; Rationale:	Deep learning baseline

Advantages:

Captures complex non-linear relationships

Automatic feature engineering

State-of-the-art performance on large datasets

Disadvantages:

Requires careful normalization

High computational cost

Black box interpretation

Clinical Rationale:

Baseline for potential complex biomarker interactions not captured by trees

## 4. Results Analysis

#### 4.1 Disease Progression Prediction

![image](https://github.com/user-attachments/assets/28e738f5-0604-4139-8417-221620780945)

Interpretation:

LightGBM: Achieved near-perfect recall (98%) crucial for not missing high-risk patients

![image](https://github.com/user-attachments/assets/c144cdf5-79b7-46e9-832d-f4dee0b49b67)

![image](https://github.com/user-attachments/assets/292cf54f-1f2d-43f9-931f-3a3c4bff4e7d)

![image](https://github.com/user-attachments/assets/f4dcb6ea-a2cf-4a68-ab97-8cf2c9e189c5)

Random Forest: Showed 100% training accuracy → Clear overfitting despite pruning

![image](https://github.com/user-attachments/assets/2c6fad40-b933-41ef-ac92-2e63ea301edd)

![image](https://github.com/user-attachments/assets/545087f3-3b4b-4a1e-b21c-597db4b98eb6)

![image](https://github.com/user-attachments/assets/f46bf05a-babe-4b9e-ac37-149002d51ae3)

DNN: Lowest performance → Insufficient data for deep feature learning

![image](https://github.com/user-attachments/assets/f1e36f6b-835c-4df6-98c6-33217d876d79)

![image](https://github.com/user-attachments/assets/8331e337-8034-408f-876d-533823d8add7)

![image](https://github.com/user-attachments/assets/e8e70b29-16c5-4df8-93c1-b780bbba3b28)

The dominance of engineered risk score validates its clinical relevance. Metastasis location weighting aligns with known survival impacts (liver > lung > peritoneal).

## 4.2 Treatment Response Prediction

![image](https://github.com/user-attachments/assets/7ec93b7a-abb6-4bdd-90bc-809b69627185)

#### Interpretation:

Random Forest: Highest accuracy but lowest AUC → Good threshold calibration

![image](https://github.com/user-attachments/assets/97f063e5-9cec-4229-9c5a-6be614182e48)

![image](https://github.com/user-attachments/assets/691973f7-fa4a-46fa-b622-ba5f7a063c5d)

![image](https://github.com/user-attachments/assets/f53d58e8-6efa-438c-a291-9b26363936d5)

LightGBM: Best AUC → Superior ranking of positive cases

![image](https://github.com/user-attachments/assets/f5dd62b4-cbf2-49ff-b945-217c6053bbbb)

![image](https://github.com/user-attachments/assets/0ac052f5-a484-4f4d-acbf-25b326b1f427)

![image](https://github.com/user-attachments/assets/95d71e89-34d8-45a1-827e-2af64abeba95)

DNN: Poor performance → Insufficient non-linear patterns

![image](https://github.com/user-attachments/assets/e8d05716-667e-4413-a85a-eb2aeb48e87d)

![image](https://github.com/user-attachments/assets/97b30c56-4c66-4765-9d99-070fb38763ee)

![image](https://github.com/user-attachments/assets/ae97e146-461f-4439-9f0a-b81614586c5a)

Requires cost-sensitive learning with asymmetric error weights

## 4.3 Immunotherapy Effectiveness

![image](https://github.com/user-attachments/assets/f8b82315-a63c-4230-a374-b6f69cb0f9e0)

#### Interpretation:

![image](https://github.com/user-attachments/assets/bba5c6f0-a21f-4a33-ba7b-86c5310fa832)

![image](https://github.com/user-attachments/assets/b1c1ba0e-1800-4392-9b4e-04e230be00c4)

![image](https://github.com/user-attachments/assets/c2791843-4c8f-4d48-80c0-8eda1b759578)

![image](https://github.com/user-attachments/assets/a9a3a199-d3ce-41e7-9284-5612bc95b82a)

![image](https://github.com/user-attachments/assets/a340dde5-ca3d-43ae-b691-8957f88a7d26)

![image](https://github.com/user-attachments/assets/f922bf54-4a52-4ab7-9d04-64b0cfa89443)

![image](https://github.com/user-attachments/assets/16b938d5-8dec-4942-b5e5-9d210c2750a8)

![image](https://github.com/user-attachments/assets/f69e58e3-e113-4222-9013-9d897a73c45f)

![image](https://github.com/user-attachments/assets/ee2531e8-c73b-4bbd-81e9-9149a9be30c8)

All models achieved >90% accuracy → EBV status is dominant predictor

LightGBM's 0.984 AUC approaches diagnostic test reliability

Aligns with recent NEJM findings on EBV+ gastric cancer responsiveness to PD-1 inhibitors

## 5. Clinical Implications

#### 5.1 Key Findings

Disease Progression can be predicted with >95% accuracy

Treatment Response remains challenging (max 81% accuracy)

EBV Status is crucial for immunotherapy predictions

Genomic Instability (FGA) significantly impacts outcomes

#### 5.2 Actionable Insights

High-risk patients (risk_score > median) need closer monitoring

HER2+ patients may benefit from targeted therapies

EBV+ patients should prioritize immunotherapy

## Conclusion

This analysis demonstrates LightGBM's superiority in clinical prediction tasks, achieving state-of-the-art performance (AUC 0.987) while maintaining computational efficiency. The framework provides a robust foundation for clinical decision support, though requires prospective validation before deployment.
