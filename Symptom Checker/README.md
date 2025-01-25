## Project Overview

This machine learning project addresses a critical healthcare challenge: early disease prediction through intelligent symptom analysis. The system uses patient profile data in probabilistic disease likelihood assessments by leveraging advanced computational techniques.

## Methodology

#### Data Preparation

Raw medical data from an Excel dataset underwent a comprehensive transformation. This involved sophisticated encoding techniques for both categorical and binary features, including:

1. Numerical feature standardization
2. Binary feature mapping (Yes/No to 1/0)
3. Categorical feature encoding
4. Dynamic risk factor computation

![image](https://github.com/user-attachments/assets/80eed818-f548-48f8-afcf-15d182d0ecbb)

#### Machine Learning Strategy

I employed a multi-model approach, training six distinct classification algorithms to maximize predictive potential:

1. CatBoost (Best Performer)
2. XGBoost
3. Random Forest
4. Logistic Regression
5. Support Vector Machine
6. LightGBM

### Performance Metrics

#### Model Accuracy Comparison

The CatBoost classifier emerged as the top performer, achieving a 42.42% accuracy rate. While this might seem modest, medical prediction is inherently complex, and the model provides probabilistic insights rather than definitive diagnoses.

#### Accuracy Comparison:

1. Logistic Regression Accuracy: 0.3030
2. Random Forest Accuracy: 0.3333
3. XGBoost Accuracy: 0.4242
4. CatBoost Accuracy: 0.4242
5. SVM Accuracy: 0.3030

![image](https://github.com/user-attachments/assets/17c24d49-860b-442d-861c-f7a7f9f2e791)

### Reasons for Low accuracy

Although the accuracy of the models is not as high as expected, one of the reasons behind it is the small dataset available for this system.

**Dataset Limitations**

1. Small dataset size
2. Limited number of samples per disease
3. Potential class imbalance
4. High variability in symptoms across diseases

**Feature Complexity**

1. Complex, non-linear relationships between symptoms and diseases
2. Limited feature set
3. Potential noise or inconsistencies in feature representation
 
**Model Constraints**

1. Relatively simple machine learning models
2. Limited hyperparameter tuning
3. No advanced ensemble techniques
4. No deep learning approach to capture complex patterns

**Recommended Improvements**

1. More diverse, larger dataset
2. Use of more sophisticated models (deep learning)
3. Implementing cross-validation
4. Domain expertise to be added

#### Gradio App

![image](https://github.com/user-attachments/assets/2f06f2e0-bddc-44e9-818d-aa59bcf1f678)

![image](https://github.com/user-attachments/assets/c3193312-b114-426a-9f6d-547156b6cbca)

A medical professional still needs to evaluate the likelihood of the diseases based on symptoms.

#### Technology Stack

1. Programming Language: Python
2. Machine Learning Libraries: Scikit-learn, XGBoost, CatBoost
3. Data Manipulation: Pandas, NumPy
4. Visualization: Matplotlib, Seaborn
5. Interface Development: Gradio

#### Conclusion

This disease prediction system represents a significant step towards leveraging machine learning for preliminary medical diagnostics, offering a probabilistic framework for identifying potential health risks based on patient profiles.
