# Sepsis Prediction from Clinical Data

This project implements a machine learning pipeline to predict the onset of sepsis in ICU patients. Using a large dataset of clinical time-series measurements obtained from PhysioNet, the goal is to build a reliable classification model that can serve as an early-warning system.

## Project Workflow

The project followed these key steps:
1.  **Data Aggregation:** Combined over 40,000 individual patient data files (`.psv`) into a single, unified dataset.
2.  **Exploratory Data Analysis (EDA):** Investigated the dataset to understand its properties, focusing on class distribution and missing data.
3.  **Preprocessing & Feature Engineering:** Cleaned the data by removing features with excessive missing values and engineered new, clinically relevant features from raw vital signs (e.g., categorizing blood pressure as 'normal', 'low', or 'high').
4.  **Handling Class Imbalance:** Addressed the severe class imbalance using the **SMOTE (Synthetic Minority Over-sampling Technique)** on the training data.
5.  **Model Training & Evaluation:** Trained four different classification models: Logistic Regression, K-Nearest Neighbors, Decision Tree, and Gaussian Naive Bayes.
6.  **Model Comparison:** Evaluated and compared the models using metrics like accuracy, precision, recall, and confusion matrices to select the best performer.

## Key Findings & EDA Insights

### 1. Severe Class Imbalance
The dataset is extremely imbalanced, with sepsis cases representing only **1.8%** of the total records. This makes accuracy a potentially misleading metric and highlights the need for techniques like SMOTE.



### 2. Extensive Missing Data
A significant challenge was the high volume of missing data. Many lab-based measurements were missing for over 95% of the entries. This necessitated a strategy of dropping the most sparse features.



### 3. Effect of SMOTE
Applying SMOTE to the training data successfully balanced the classes, creating a 50/50 split between sepsis and non-sepsis cases. This ensures the models do not simply learn to predict the majority class.



## Model Performance & Results

All four models were trained on the SMOTE-balanced training set and evaluated on the original, imbalanced test set to simulate real-world conditions.

#### Performance Metrics Summary

| Model                 | Accuracy | Precision | Recall | Avg Precision |
| --------------------- | :------: | :-------: | :----: | :-----------: |
| **Decision Tree**     | **0.9501** |  0.1261   | 0.2989 |    0.0503     |
| K-Nearest Neighbors   |  0.9389  |  0.1278   | 0.4120 |    0.0632     |
| Gaussian Naive Bayes  |  0.8215  |  0.0454   | 0.4455 |    0.0302     |
| Logistic Regression   |  0.7773  |  0.0430   | 0.5352 |    0.0314     |

#### Model Accuracy Comparison

The Decision Tree model achieved the highest overall accuracy of 95.01%.



#### Confusion Matrices & Interpretation

While the Decision Tree model has the highest accuracy, its **recall is low (0.2989)**. This means it correctly identifies only about 30% of actual sepsis cases, while missing the other 70% (4,893 false negatives).



## Conclusion

The project successfully demonstrates a full pipeline for a complex clinical prediction task. The **Decision Tree model was the best performer based on accuracy**.

The models are not yet reliable for clinical use because they fail to identify a large proportion of sepsis patients (high false negatives).

**Future work should focus on improving recall**, potentially through more advanced feature engineering, using Deep Learning algorithms, or tuning model parameters to penalize false negatives more heavily.
