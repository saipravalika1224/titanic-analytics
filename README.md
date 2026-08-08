# Analytics Pipeline Report — Module 2

## 1. Missing-Value Handling Strategy
- *deck (77.21% missing)*: Exceeds 30% threshold. Imputation is unreliable; dropping removes over 75% of data. Encoded missing values explicitly as category "Unknown".
- *age (19.87% missing)*: Falls in 5%–30% threshold. Imputed with median age to prevent skewing from older outliers.
- *embarked / embark_town (0.22% missing)*: Under 5% threshold. Dropped missing rows.

## 2. Univariate & Skewness Analysis
- *Age Outliers (IQR)*: 24 outliers identified.
- *Fare Outliers (IQR)*: 116 outliers identified due to high luxury class ticket pricing.
- *Fare Skewness*: Right-skewed ($\text{Mean} > \text{Median} > \text{Mode}$).

## 3. Bivariate Correlations
1. *pclass vs fare ($r = -0.55$)*: Strong negative correlation reflecting high class tickets cost significantly more.
2. *pclass vs survived ($r = -0.34$)*: Moderate negative correlation showing higher class passengers had superior survival rates.

## 4. Multivariate Data Story Summary
- *Chart 1 (Sex & Class)*: Female survival exceeded 90% in 1st/2nd class, while 3rd class male survival dropped below 15%.
- *Chart 2 (Age & Class)*: Children in 1st/2nd class were prioritized during evacuation.
- *Chart 3 (Fare vs Age Scatter)*: Passengers paying high fares ($>\$100$) were overwhelmingly survivors.
- *Chart 4 (Family Size)*: Solo travelers and families $>4$ faced higher mortality; mid-sized families (2–4) had highest survival rates.

## 5. Model Comparison Summary

| Metric Group | Model Candidate | Accuracy / MAE | Precision / RMSE | Recall / R² | F1 Score / Adj R² | AUC |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| *Classification* | Logistic Regression | 0.804 | 0.771 | 0.710 | 0.739 | 0.852 |
| | Decision Tree | 0.793 | 0.789 | 0.652 | 0.714 | 0.811 |
| | *Tuned Random Forest* | *0.827* | *0.812* | *0.725* | *0.766* | *0.874* |
| *Regression* | Linear Regression (fare) | MAE: 18.24 | RMSE: 34.12 | R²: 0.385 | Adj R²: 0.379 | N/A |

## 6. Fare Regression Heteroscedasticity
The residual plot displays an expanding fan-shaped distribution as predicted fare increases. This confirms *heteroscedasticity*, as high-value ticket fares introduce significantly greater variance than standard ticket fares.

## 7. Deployment Recommendation
Deploy the *Tuned Random Forest Pipeline. It achieved the top overall metrics with an **F1 score of 0.766* and *AUC of 0.874*. Its non-parametric tree structure accurately captures complex non-linear feature interactions without data leakage.