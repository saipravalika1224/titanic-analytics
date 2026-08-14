# Module 2 — Analytics Pipeline (/analytics)

## 1. Missing Value Handling Summary
* *deck (77.22% missing):* Dropped column. Imputation above 30% introduces significant bias.
* *age (19.87% missing):* Median imputed by pclass (5%–30% threshold rule).
* *embarked / embark_town (0.22% missing):* Dropped affected rows (<5% threshold rule).

---

## 2. EDA & Skewness Analysis
* *Age Outliers (IQR):* 27
* *Fare Outliers (IQR):* 114
* *Fare Distribution:* Right-skewed (Mean: 32.10 > Median: 14.45 > Mode: 8.05).

### Top 2 Off-Diagonal Correlations
1. *pclass vs. fare (r = -0.55):* Strongest correlation; higher numerical class tiers (3rd class) cost significantly less.
2. *pclass vs. age (r = -0.41):* Older passengers disproportionately occupied higher socio-economic tiers (1st class).

---

## 3. Multivariate Data Story
1. *Sex & Pclass vs. Survival:* Female passengers in 1st/2nd class had >85% survival, while 3rd class males had <15%.
2. *Age & Fare vs. Survival:* Outlier ticket purchases (>200) showed near-complete survival across ages.
3. *Family Size vs. Survival:* Solo travelers and large families (>4) had lower survival rates than small family units (2–4).
4. *Age Distribution Across Classes:* Children (0–10) had high survival in 1st/2nd class but lower survival in 3rd class.

---

## 4. Modeling & Performance Comparison

| Model Type | Model Name | Accuracy | Precision | Recall | F1 Score | ROC-AUC | MAE | RMSE | R² | Adj R² |
| :--- | :--- | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| *Classifier* | Logistic Regression | 0.8045 | 0.7681 | 0.7162 | 0.7413 | 0.8542 | — | — | — | — |
| *Classifier* | Decision Tree | 0.7989 | 0.8148 | 0.6111 | 0.6984 | 0.8210 | — | — | — | — |
| *Classifier* | *Random Forest (Tuned)* | *0.8268* | *0.8125* | *0.7222* | *0.7647* | *0.8681* | — | — | — | — |
| *Regressor* | Multivariate Linear Reg. | — | — | — | — | — | 19.12 | 35.45 | 0.3821 | 0.3415 |

### Class Imbalance & Regression Conclusions
* *Imbalance Handling:* class_weight='balanced' and SMOTE improved recall slightly, but baseline/tuned Random Forest maintained the best overall F1 score balance.
* *Regression Heteroscedasticity:* Residual plot for fare prediction showed clear heteroscedasticity due to extreme high-fare ticket outliers.

---

## 5. Final Recommendation
We recommend deploying the *Tuned Random Forest Classifier* (Accuracy: 82.68%, F1 Score: 0.7647, ROC-AUC: 0.8681) as it best captures complex non-linear feature interactions without overfitting.
