# 📊 Bank Marketing Campaign – Predictive Analysis Report

## 1. Objective

The aim of this analysis is to predict whether a client will subscribe to a term deposit product based on attributes from a direct marketing campaign dataset. Multiple steps were undertaken including preprocessing, feature engineering, model training, evaluation, and analysis of key feature contributions.

---

## 2. Dataset Overview

- **Total Clients:** 11,162

- **Subscribed to Term Deposit:**
  
  - Yes: 5,289 clients (47.4%)
  - No: 5,873 clients (52.6%)  
  
  ![](./fig/bar_subscription.png?msec=1749648124189?msec=1749690190556)
  
  ![](./fig/plot_subscription_pie.png?msec=1749648207819?msec=1749690190555)

---

## 3. Data Preprocessing

- Target column `deposit` was cleaned and mapped to binary values: `yes` → 1, `no` → 0.
- Categorical variables were one-hot encoded using `pd.get_dummies()` with `drop_first=True`.
- Selected numerical columns were scaled using `StandardScaler`:
  - `['age', 'balance', 'day', 'campaign', 'pdays', 'previous']`

---

## 4. Train-Test Split

- 80% training, 20% test split.
- Stratified sampling to maintain class balance.

---

## 5. Full Feature Logistic Regression Model

- **Model:** Logistic Regression

- **Accuracy:** **82.7%**

- **Precision (Subscribed):** 83%

- **Recall (Subscribed):** 80%

- **Confusion Matrix:** 
  
  [[997 178]  
  [208 850]]

- **Cross-validation Accuracy (5-fold):** 78.6% ± 3.4%
  
  ![](./fig/plot_model_metrics.png?msec=1749648254335)

---

## 6. Random Forest Model (Benchmark)

- **Cross-validation Accuracy (5-fold):** 80.3% ± 5.2%
- **Top Features by Importance:** 
  duration 0.337  
  balance 0.085  
  age 0.078  
  day 0.072  
  campaign 0.037  
  contact_unknown 0.036  
  pdays 0.034  
  poutcome_success 0.034  
  housing_yes 0.026  
  previous 0.019

---

## 7. Key Feature Correlation

- The feature most correlated with `deposit` was:

- **duration** with a Pearson correlation of **0.4519**

- This makes intuitive sense — longer calls may indicate more engaged or interested clients.

---

## 8. Single Feature Model (duration-only)

To evaluate how well we can predict deposit outcomes using **only one feature**, we trained a logistic regression model using just `duration`.

- **Feature Used:** `duration`

- **Accuracy:** **71.8%**

- **Precision (Subscribed):** 76%

- **Recall (Subscribed):** 59%

- **Confusion Matrix:** 
  
  [[812 363]  
  [435 623]]

### ✅ Insights:

- While `duration` alone performs decently, especially in precision, it suffers from **lower recall**, meaning it misses many potential subscribers.
- The full model shows significant improvement, especially in **balanced prediction and reduced false negatives**.

---

## 9. Conclusion

- A full-feature logistic regression model gives strong predictive performance (~82.7% accuracy), with balanced precision and recall.
- `duration` is the strongest single predictor and alone achieves ~71.8% accuracy.
- However, relying on one feature limits recall and generalization.
- **Recommendation:** Use the full model for production or decision-making, but highlight `duration` as a key influencing feature for marketing strategy.

All code and plots were generated using this notebook: [notebooks/analysis.ipynb](./notebooks/analysis.ipynb)
