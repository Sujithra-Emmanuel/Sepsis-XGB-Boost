**🧬 Sepsis-XGB-Boost**

Early detection of sepsis can significantly reduce complications and save lives. This project explores the application of XGBoost, a powerful machine learning algorithm, to build an early warning system for sepsis prediction using ICU data.

**🚨 Problem Overview**

Sepsis is a life-threatening condition triggered by the body’s extreme response to infection. It can lead to tissue damage, organ failure, and death. Prompt diagnosis and treatment are essential — every hour of delayed antibiotic treatment increases mortality by 7.6%.

**❗ Limitations of Traditional Detection Methods**
Common clinical scoring systems like:

SOFA (Sequential Organ Failure Assessment)
qSOFA (Quick SOFA)
SIRS (Systemic Inflammatory Response Syndrome)
NEWS and cNEWS (National Early Warning Scores)
...are widely used, but fall short in early detection due to:

Inability to capture complex, subtle physiological patterns
Delays in response time

**💡 Why Machine Learning?**

With the availability of Electronic Health Records (EHRs) and real-time ICU data, machine learning offers:
Faster identification of at-risk patients
Greater accuracy using temporal patterns
Potential to augment traditional clinical judgment

**📊 Dataset Overview**

Size: 1,552,210 hourly records
Patients: 40,336 ICU patients across 2 hospitals
Features:
Vital signs
Lab test results
Patient demographics
Binary sepsis labels
⚠️ Missing Data: 65.19% of values were missing
➡️ Managed using forward-fill imputation to maintain temporal integrity.

**🧪 Data Preprocessing**

❌ Feature Removal: Dropped features with >99% missing values
🔁 Forward Fill: Imputed missing values using previous valid entries
🧬 Feature Engineering: Extracted clinical scores, vital signs, lab values, demographics
⚖️ Class Balancing: Downsampled majority class (non-sepsis) to reduce bias

**🔬 Biomarker Correlation**

Pearson and Spearman correlations were calculated
Helped reduce feature redundancy and select informative predictors

**🚀 Model: XGBoost**

Chosen for:
Efficiency with structured data
Robustness to missing values and multicollinearity
Built-in regularization to reduce overfitting

**🔧 Model Training**

Class Imbalance Handling: Downsampling majority class
**Hyperparameter Tuning:**
Method: Bayesian Optimization (TPE)
Parameters:
Max Depth
Learning Rate
Subsample Ratio
Feature Sampling
L1, L2 Regularization
**Training Strategy:**
5-fold Cross-Validation
Early Stopping
Ensemble Learning (average predictions from 5 models)

**📈 Evaluation Metrics**

Metric	Score	Notes
Accuracy	77.25%	Solid overall performance
Recall	74%	High recall = better sepsis detection
Precision	5.62%	Low due to class imbalance
AUROC	0.8314	Excellent class separation
AUPRC	0.1133	Reflects challenge in detecting minority class
⚠️ Low Precision: Points to need for further class balancing and optimization

**📌 Key Challenges**

⚖️ Class Imbalance: Hinders model precision
📉 Missing Data: Incomplete records reduce reliability
🕒 Sensitivity to Time: Sepsis progression is rapid and time-sensitive

**🛠 Future Improvements**

🔄 Advanced Imputation: Try model-based or multi-feature imputations
👤 Personalization: Account for genetic, demographic, and treatment variability
⏱ ICULOS (ICU Length of Stay): A key predictor — explore further integration


**✅ Conclusion**

This project demonstrates that XGBoost can effectively predict early signs of sepsis with high recall. While challenges remain (notably class imbalance and missing data), the approach represents a critical step toward ML-integrated clinical decision support systems that improve ICU outcomes.
