# ENSEMBLE METHODS FOR BREAST CANCER CLASSIFICATION

## AUTHORS
1. Norman Mwapea
2. Kiprono Langat
3. Pauline Kariuki
4. Judith
5. Alvin
6. Wesley

## PROJECT OVERVIEW
Ensemble learning lies at the heart of modern machine learning. Instead of relying on a single model, ensembles combine the strengths of multiple learners, reducing weaknesses and improving overall predictive performance.  

This project demonstrates the application of **Decision Trees, Random Forests, and XGBoost** on the **Breast Cancer Wisconsin dataset** (from scikit-learn). We evaluate each model’s performance under different conditions, including class imbalance handling and hyperparameter tuning, to determine the most reliable classifier.

## METHODOLOGY

### 1. **Data Understanding**

- Dataset: Breast Cancer Wisconsin dataset (569 records, 30 features + target).
- Target:  
  - **1 → Malignant**  
  - **0 → Benign**  
- Observations:  
  - Features are numeric.  
  - Data is clean (no missing values or duplicates).  
  - Class imbalance present (62% malignant vs 38% benign).  

### 2. **Data Preprocessing**

- Standardization using **StandardScaler**.  
- Log transformations applied to highly skewed features.  
- Addressed imbalance using:  
  - **Class Weights**  
  - **SMOTE (Synthetic Minority Oversampling Technique)**  

### 3. **Modeling Approaches**

We implemented three main ensemble methods:
1. **Decision Trees** – baseline interpretable model.  
2. **Random Forests** – averaging across many trees to improve stability.  
3. **XGBoost** – gradient boosting for high performance.  

Each model was trained under three scenarios:
- **Vanilla models** (default hyperparameters).  
- **Weighted models** (using class weights).  
- **SMOTE models** (trained on resampled balanced data).  

### 4. **Hyperparameter Tuning**

- GridSearchCV and RandomizedSearchCV applied to Random Forest and XGBoost.  
- Best models selected based on accuracy, precision, recall, F1-score, and ROC-AUC.  

## RESULTS SUMMARY

| Model          | Variant   | Accuracy | Recall (Malignant) | AUC   |
|----------------|-----------|----------|---------------------|-------|
| Decision Tree  | Vanilla   | 89%      | 0.88                | 0.890 |
|                | Weighted  | 91%      | 0.90                | 0.937 |
|                | SMOTE     | 93%      | 0.93                | 0.930 |
| Random Forest  | Vanilla   | 96%      | 0.97                | 0.991 |
|                | Weighted  | 94%      | 0.94                | 0.993 |
|                | SMOTE     | 93%      | 0.93                | 0.994 |
| XGBoost        | Vanilla   | 95%      | 0.97                | 0.990 |
|                | Weighted  | 96%      | **0.99**            | 0.994 |
|                | SMOTE     | 95%      | 0.97                | 0.995 |


**Key Insights**:
- **Random Forest** achieved the most consistent performance (96% accuracy, 0.97 recall).  
- **Weighted XGBoost** minimized false negatives with **0.99 recall**, critical for medical diagnosis.  
- **Decision Trees** remain interpretable but underperform compared to ensemble methods.  

## CONCLUSIONS
- **Random Forests** provide the most balanced and stable performance, making them ideal for general deployment.  
- **Weighted XGBoost** is preferable in clinical contexts where missing malignant cases could have severe consequences.  
- **Decision Trees** are useful for interpretability but trade off accuracy and recall.  

## RECOMMENDATIONS
1. **Best Overall Model**: Deploy **Random Forest with tuning** for reliability and stability.  
2. **For Clinical Use**: Use **Weighted XGBoost**, since it reduces false negatives and maximizes malignant detection.  
3. **Model Maintenance**:  
   - Continuously retrain models with new patient data.  
   - Apply hyperparameter tuning periodically.  
   - Use early stopping (XGBoost) and max depth control (Random Forest) to avoid overfitting.  
4. **Interpretability**: Pair ensemble models with tools like **SHAP** or **LIME** for explainable predictions.  
5. **Future Work**:  
   - Explore other boosting frameworks (LightGBM, CatBoost).  
   - Expand evaluation with larger, real-world healthcare datasets.  
   - Develop a stacking ensemble combining Random Forest and XGBoost.  
