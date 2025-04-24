# Fraud Detection System

This repository contains a machine learning-based fraud detection system that predicts fraudulent transactions. It focuses on identifying suspicious activities in financial transactions, which can help companies detect and prevent fraudulent activities in real-time.

## Table of Contents
1. [Overview](#overview)
2. [Data Cleaning](#data-cleaning)
3. [Fraud Detection Model](#fraud-detection-model)
4. [Variable Selection](#variable-selection)
5. [Model Performance](#model-performance)
6. [Key Factors Predicting Fraudulent Transactions](#key-factors-predicting-fraudulent-transactions)
7. [Prevention Strategies](#prevention-strategies)
8. [How to Use](#how-to-use)
9. [Future Improvements](#future-improvements)
10. [Conclusion]

## Overview

The project involves building a machine learning model for detecting fraudulent transactions. The model uses a **Neural Network** architecture to predict whether a transaction is fraudulent based on various features of the transaction. The model is trained using a large dataset containing transaction information, and it has been optimized to handle class imbalance using techniques like **SMOTE**.

## Data Cleaning

Data cleaning is a critical step before building any predictive model. Here’s how it was handled in this case:

### Missing Values:
- Missing values in numerical columns were handled by **imputation** using the **mean** or **median** depending on the distribution of the data.
- Categorical columns with missing values were imputed using the **mode**.
- Columns with a high percentage of missing data were removed.

### Outliers:
- Outliers were detected using **IQR** (Inter-Quartile Range) and visualizations like **box plots**.
- Extreme outliers were removed, while other unusual values were capped to preserve important insights.

### Multi-collinearity:
- Multi-collinearity was detected using **Variance Inflation Factor (VIF)**.
- Features with a VIF higher than a threshold (e.g., 5) were removed to reduce multicollinearity.

## Fraud Detection Model

The fraud detection model is based on a **Neural Network (NN)** architecture. Here's a detailed description:

### Data Preprocessing:
- The data was scaled using **StandardScaler** to ensure features have a mean of 0 and variance of 1, which is crucial for neural networks.

### Model Architecture:
- **Input Layer**: The model has an input layer corresponding to the number of features (14 features).
- **Hidden Layers**: Two dense layers with **128** and **64** neurons respectively, activated by **ReLU** (Rectified Linear Unit).
- **Dropout Layers**: A dropout rate of **0.5** was used to prevent overfitting.
- **Output Layer**: A single neuron activated by **sigmoid** for binary classification (fraud vs. non-fraud).
  
### Optimizer and Loss Function:
- The model used the **Adam optimizer** and **binary crossentropy** as the loss function.

### Evaluation:
- Model performance was evaluated using **precision**, **recall**, **F1-score**, **ROC-AUC**, and **confusion matrix**.
- **SMOTE** was used to balance the dataset due to class imbalance.

## Variable Selection

The features were selected based on domain knowledge and statistical techniques:

- **Domain Knowledge**: Features like `amount`, `oldbalanceOrg`, `newbalanceOrig`, `nameDest`, and `nameOrig` were selected because they directly relate to transactional activities.
- **Correlation Analysis**: Highly correlated features (e.g., `oldbalanceOrg` and `newbalanceOrig`) were reduced to avoid multicollinearity.
- **Feature Engineering**: New features like `errorBalanceOrig`, `isMerchant`, `isHighAmount`, and `netBalanceChange` were created for better predictive power.

## Model Performance

The performance of the model was evaluated using various metrics:

### Classification Report:
- **Precision**: 0.44 for fraudulent transactions.
- **Recall**: 0.99 for fraudulent transactions.
- **F1-Score**: 0.61 for fraudulent transactions.
- **ROC-AUC**: 0.997, indicating excellent discrimination between fraud and non-fraud.

### Confusion Matrix:

The confusion matrix provides a visual representation of the model's performance, showing how well the model is classifying fraudulent and non-fraudulent transactions:
|                     | Predicted Non-Fraud | Predicted Fraud |
|---------------------|---------------------|-----------------|
| **Actual Non-Fraud**| 825,546 (TN)        | 3,113 (FP)      |
| **Actual Fraud**    | 15 (FN)             | 2,449 (TP)      |
## Key Factors Predicting Fraudulent Transactions

- **Amount**: Large or unusual transaction amounts.
- **Error Balances**: Significant mismatches between `oldbalanceOrg` and `newbalanceOrig`.
- **Merchant Transactions**: High-value transactions flagged when `isMerchant` is true.
- **Transfer Ratio**: Large transfer-to-balance ratios are indicative of potential fraud.
- **Destination Balance Not Updated**: If the destination balance isn't updated post-transaction, it may signal fraud.

## Prevention Strategies

To prevent fraud in the future, the following strategies can be adopted:

1. **Real-Time Monitoring**: Implement real-time anomaly detection systems using AI/ML models.
2. **User Authentication**: Enforce two-factor authentication for large transactions or those made from unfamiliar locations.
3. **Transaction Limits**: Place limits on transactions above certain thresholds, especially during unusual hours.
4. **Transaction History Analysis**: Continuously monitor customer transaction history for anomalies.


## Conclusion: 
Fraud detection is an ongoing challenge that requires careful model selection, feature engineering, and continuous monitoring. By focusing on the right features, utilizing advanced models like neural networks, and adopting preventive measures in infrastructure, the company can significantly reduce the occurrence of fraudulent transactions. Regular evaluation and improvements to the model will be essential for keeping up with evolving fraud tactics.

