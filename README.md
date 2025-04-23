
# 🧬 Sepsis-XGB-Boost

Early detection of sepsis can significantly reduce complications and save lives. This project explores the application of **XGBoost**, a powerful machine learning algorithm, to build an early warning system for **sepsis prediction** using ICU data.

🔗 **Interactive Dashboard:** [View Sepsis Dashboard](https://public.tableau.com/app/profile/sujithra.emmanuel/viz/XGBBOOSTEARLYDETECTIONOFSEPIS/DMAINNight)

---

## 🚨 Problem Overview

**Sepsis** is a life-threatening condition triggered by the body’s extreme response to infection. It can lead to tissue damage, organ failure, and death. Prompt diagnosis and treatment are essential — **every hour of delayed antibiotic treatment increases mortality by 7.6%**.

### ❗ Limitations of Traditional Detection Methods

Common clinical scoring systems like:

- SOFA (Sequential Organ Failure Assessment)
- qSOFA (Quick SOFA)
- SIRS (Systemic Inflammatory Response Syndrome)
- NEWS and cNEWS (National Early Warning Scores)

...are widely used, but **fall short in early detection** due to:

- Inability to capture complex, subtle physiological patterns
- Delays in response time

---

## 💡 Why Machine Learning?

With the availability of **Electronic Health Records (EHRs)** and **real-time ICU data**, machine learning offers:

- Faster identification of at-risk patients
- Greater accuracy using temporal patterns
- Potential to augment traditional clinical judgment

---

## 📊 Dataset Overview

- **Size:** 1,552,210 hourly records  
- **Patients:** 40,336 ICU patients across 2 hospitals  
- **Features:**
  - Vital signs
  - Lab test results
  - Patient demographics
  - Binary sepsis labels

> ⚠️ **Missing Data:** 65.19% of values were missing  
> Managed using **forward-fill imputation** to maintain temporal integrity.

---

## 🧪 Data Preprocessing

- ❌ Feature Removal: Dropped variables with >99% missing values  
- 🔁 Forward Fill: Imputed missing values using recent valid values  
- 🧬 Feature Engineering: Extracted vital signs, lab values, clinical scores, and demographics  
- ⚖️ Class Balancing: Downsampled majority class (non-sepsis) for balanced training

---

## 🔬 Biomarker Correlation

- Computed **Pearson** and **Spearman** correlation matrices
- Helped identify key predictors and remove redundant features

---

## 🚀 Model: XGBoost

**Why XGBoost?**

- Efficient for structured data
- Handles missing values natively
- Regularization prevents overfitting
- Robust to multicollinearity

---

## 🔧 Model Training and Optimization

- **Class Imbalance Handling:** Downsampling of majority class  
- **Hyperparameter Tuning:**
  - Method: Bayesian Optimization (TPE)
  - Tuned Parameters:
    - Maximum Tree Depth
    - Learning Rate
    - Subsample Ratio
    - Feature Sampling Ratio
    - L1 and L2 Regularization Terms

- **Training Strategy:**
  - 5-Fold Cross-Validation
  - Early Stopping
  - Ensemble Learning: Averaged outputs from 5 trained models

---

## 📈 Evaluation Metrics

| Metric     | Score     | Notes                                        |
|------------|-----------|----------------------------------------------|
| Accuracy   | 77.25%    | Solid overall performance                    |
| Recall     | 74%       | High recall = better sepsis detection        |
| Precision  | 5.62%     | Low due to class imbalance                   |
| AUROC      | 0.8314    | Excellent class separation                   |
| AUPRC      | 0.1133    | Reflects difficulty in minority class detection |

> ⚠️ **Low Precision** highlights need for improved balancing or alternative strategies.

---

## 📌 Key Challenges

- ⚖️ **Class Imbalance:** Impacts model precision  
- 📉 **Missing Data:** Reduces reliability and interpretability  
- ⏱️ **Time Sensitivity:** Sepsis progression requires temporal awareness

---

## ✅ Conclusion

This XGBoost-powered early warning system demonstrates the potential of **machine learning** in **early sepsis detection**. With strong recall and class separation, it represents a promising direction for integrating predictive models into critical care workflows.

---


