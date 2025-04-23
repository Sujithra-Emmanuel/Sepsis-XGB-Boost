# Sepsis-XGB-Boost
Sepsis is a severe medical condition that arises when the body’s response to infection triggers widespread inflammation, leading to organ dysfunction, shock, and often, death. It remains one of the leading causes of hospitalization and in-hospital mortality.
Prompt recognition and treatment are vital to improving patient outcomes, but delayed diagnosis significantly raises the risk of mortality. Studies have shown that each hour of delayed antibiotic treatment increases mortality by 7.6%.
Early detection plays a crucial role in preventing the escalation of sepsis and ultimately reducing mortality rates in hospitals.
The Challenge of Traditional Sepsis Detection
Traditional clinical scoring systems — such as the Sequential Organ Failure Assessment (SOFA), Quick SOFA (qSOFA), Systemic Inflammatory Response Syndrome (SIRS), National Early Warning Score (NEWS), and Critical NEWS (cNEWS) — are commonly used to assess sepsis risk.
While useful, these scoring systems often fall short in the early detection of sepsis. They lack the ability to capture complex, subtle patterns in physiological data needed for early diagnosis.
With the rise of machine learning (ML) and increased availability of electronic health records (EHRs), there’s an opportunity to develop data-driven models that can detect sepsis earlier and more accurately.
Challenges in Early Sepsis Prediction
Despite the promise of ML, early prediction of sepsis remains a challenge due to:
Overlapping Symptoms: Sepsis shares many signs with other medical conditions, making it hard to differentiate.
Heterogeneous Presentation: Different infections, genetics, and immune responses cause sepsis to manifest differently across patients.
High Volume of Missing Data: ICUs produce vast data streams, but many lab results and vitals are missing or inconsistently recorded.
Time Dependency: Sepsis progresses rapidly, requiring models that understand the time-sensitive nature of patient data
Dataset Overview
This study used a dataset of 1,552,210 data points from 40,336 ICU patients across two hospitals. It includes hourly measurements of:
Vital signs
Lab test results
Patient demographics
Sepsis status (binary label)
Notably, 65.19% of the data values were missing due to irregular test timings and equipment constraints. To manage this, a forward-fill imputation strategy was applied, ensuring temporal consistency without introducing imputation bias.
Data Preprocessing and Feature Engineering
The following steps were taken to prepare the data:
Feature Removal: Variables with >99% missing values were excluded.
Forward-Fill Imputation: Recent valid values were carried forward in the time series.
Feature Extraction: Demographics, vitals, lab values, and calculated clinical scores were selected.
Class Balancing: The non-sepsis (majority) class was downsampled to match the sepsis (minority) class, allowing the model to better learn sepsis patterns.
Normalized Biomarker Correlation
Both Pearson and Spearman correlation matrices were generated to explore relationships between biomarkers. This helped identify useful predictors and reduce redundancy among features.

XGBoost Model Training and Hyperparameter Optimization
XGBoost was selected for its ability to handle large, structured datasets efficiently, its robustness to multicollinearity, and its built-in handling of missing values. Its regularization capabilities also help reduce overfitting, making it a strong choice for clinical prediction tasks.
To address the imbalance between the majority (non-sepsis) and minority (sepsis) classes, downsampling techniques were applied to reduce the dominance of the majority class and improve model sensitivity.
Hyperparameters were optimized using Bayesian Optimization to efficiently explore the search space, while 5-fold cross-validation ensured the model’s generalizability. Early stopping was used during training to prevent overfitting. To further enhance predictive stability, ensemble learning was employed by averaging the outputs of five independently trained models.
Hyperparameter Tuning
Bayesian Optimization using the Tree-structured Parzen Estimator (TPE) was used to tune:
Maximum tree depth
Learning rate
Subsample ratio
Feature sampling ratio per boosting round
L1 and L2 regularization terms
Training Strategy
5-fold cross-validation ensured generalization.
Early stopping prevented overfitting.
Ensemble learning averaged outputs from five models for robust predictions.
Model Evaluation and Results
The model was assessed using several performance metrics:
Accuracy: 77.25%
Recall: 74% — crucial for detecting sepsis cases
Precision: 5.62% — low due to class imbalance
AUROC: 0.8314 — strong class separation ability
AUPRC: 0.1133 — reflects difficulty in minority class detection
⚠️ Note: While the model performed well in recall and AUROC, its low precision points to the need for better class balancing or alternative strategies.
Discussion and Future Work
Despite encouraging results, several challenges remain:
Key Challenges
Class Imbalance: The imbalance between septic and non-septic patients hinders precision.
Missing Data: Gaps in lab and vitals data reduce the model’s reliability.
Sensitivity: There’s room to improve the model’s early alert capability.
Potential Improvements
Enhanced Imputation Techniques: Moving beyond forward-fill to model-based imputation may improve accuracy.
Personalization: Considering genetic, treatment, and demographic variations could yield better predictions.
ICULOS Feature: ICU length of stay (ICULOS) significantly influenced predictions. Further investigation into its role could enhance model performance.
Conclusion
This XGBoost-powered early warning system offers a promising approach to early sepsis detection, especially given its high recall. It represents a step toward integrating machine learning with clinical workflows to reduce sepsis-related complications and mortality.
