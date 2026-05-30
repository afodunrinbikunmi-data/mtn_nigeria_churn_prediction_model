# mtn_nigeria_churn_prediction_model
Machine Learning for Telecom Customer Retention | Python | Scikit-Learn

## Project Summary
A machine learning project built on top of the MTN Nigeria Customer
Churn Analysis dataset. Three classification models — Logistic
Regression, Decision Tree, and Random Forest — were trained and
evaluated to predict which customers are most likely to churn,
enabling proactive retention interventions.

**Key finding: All three models expose a class imbalance problem
that limits churn recall — the most important metric for retention.
Random Forest performs best with 72.82% accuracy and 50% precision
on churned customers but misses 89% of actual churners.**

## Problem Statement
With a 29.16% churn rate and ₦58M in lost revenue, MTN Nigeria
needs to identify at-risk customers before they churn — not after.
This project builds and evaluates churn prediction models that
assign a probability score to every active customer, enabling
targeted retention campaigns based on data rather than guesswork.

## Dataset Overview
| Field | Detail |
|---|---|
| Records | 974 customer entries |
| Target Variable | Customer_Churn_Status (Yes/No) |
| Class Distribution | 70.84% Active, 29.16% Churned |
| Train/Test Split | 80% / 20% |
| Training records | 779 |
| Test records | 195 |

## Features Used
| Feature | Type |
|---|---|
| Age | Numeric |
| Satisfaction_Rate | Numeric |
| Customer_Tenure_in_months | Numeric |
| Unit_Price | Numeric |
| Data_Usage | Numeric |
| Number_of_Times_Purchased | Numeric |
| Total_Revenue | Numeric |
| High_Value | Binary (engineered) |
| Device_Encoded | Categorical (encoded) |
| Gender_Encoded | Categorical (encoded) |
| Plan_Encoded | Categorical (encoded) |

## Models Trained

### Model 1 — Logistic Regression
| Metric | Active (0) | Churned (1) |
|---|---|---|
| Precision | 0.73 | 0.00 |
| Recall | 0.99 | 0.00 |
| F1-Score | 0.84 | 0.00 |

Overall Accuracy: 72.31%

**Confusion Matrix:**
| | Predicted Active | Predicted Churned |
|---|---|---|
| Actual Active | 141 | 1 |
| Actual Churned | 53 | 0 |

**Verdict:** High accuracy but completely blind to churned customers. Classic class imbalance failure.

### Model 2 — Decision Tree (max_depth=5)
| Metric | Active (0) | Churned (1) |
|---|---|---|
| Precision | 0.74 | 0.34 |
| Recall | 0.85 | 0.21 |
| F1-Score | 0.79 | 0.26 |

Overall Accuracy: 67.69%

**Confusion Matrix:**
| | Predicted Active | Predicted Churned |
|---|---|---|
| Actual Active | 121 | 21 |
| Actual Churned | 42 | 11 |

**Verdict:** Lower accuracy but more useful — detects some churn. Customer Tenure dominates feature importance at 48%.

### Model 3 — Random Forest (n_estimators=100, class_weight='balanced')
| Metric | Active (0) | Churned (1) |
|---|---|---|
| Precision | 0.74 | 0.50 |
| Recall | 0.96 | 0.11 |
| F1-Score | 0.84 | 0.18 |

Overall Accuracy: 72.82%

**Confusion Matrix:**
| | Predicted Active | Predicted Churned |
|---|---|---|
| Actual Active | 116 | 26 |
| Actual Churned | 31 | 22 |

**Verdict:** Best overall model — highest accuracy, best churn precision, most balanced feature importance.

## Model Comparison

| Model | Accuracy | Churn Precision | Churn Recall | Churn F1 | Churned Detected |
|---|---|---|---|---|---|
| Logistic Regression | 72.31% | 0.00 | 0.00 | 0.00 | 0 of 53 |
| Decision Tree | 67.69% | 0.34 | 0.21 | 0.26 | 11 of 53 |
| Random Forest | 72.82% | 0.50 | 0.11 | 0.18 | 22 of 53 |

**Winner: Random Forest**

## Feature Importance — Random Forest (Most Reliable)

| Rank | Feature | Importance |
|---|---|---|
| 1 | Age | 0.1864 |
| 2 | Customer Tenure | 0.1591 |
| 3 | Total Revenue | 0.1514 |
| 4 | Data Usage | 0.1467 |
| 5 | Number of Purchases | 0.0926 |
| 6 | Satisfaction Rate | 0.0739 |
| 7 | Subscription Plan | 0.0721 |
| 8 | Unit Price | 0.0628 |
| 9 | Device Type | 0.0227 |
| 10 | Gender | 0.0226 |
| 11 | High Value | 0.0096 |

## Key Findings
- **Accuracy is misleading** — Logistic Regression's 72.31% accuracy detected 0 churned customers
- **Class imbalance is the core problem** — 70.84% active vs 29.16% churned limits all models
- **Random Forest is the best model** — highest precision, most churned customers detected
- **Age and Tenure are top predictors** — behavioural signals outperform satisfaction scores
- **All models need improvement** — SMOTE and XGBoost are recommended next steps

## Limitations
The dataset contains only 974 records which limits model robustness and generalisation. The class imbalance of 70/30 causes all three models to underperform on the minority churned class — the most important class for the business use case. The dataset is synthetically generated and results should not be applied to real MTN Nigeria business decisions without validation on live customer data.

## Next Steps
- Implement SMOTE to balance training data
- Test XGBoost with scale_pos_weight parameter
- Tune classification threshold to optimise churn recall
- Collect more data to improve model generalisation
- 
## Repository Structure
```text
├── data/
│   ├── mtn_customers.csv
│   └── mtn_customers_enriched.csv
├── notebooks/
│   └── mtn_churn_prediction.ipynb
├── results/
│   ├── logistic_regression_results.png
│   ├── decision_tree_results.png
│   └── random_forest_results.png
└── README.md
```

## About me
Afodunrinbi Samad Akinkunmi

I am a Certified Data Analyst with a strong passion for transforming raw data into meaningful insightsand building predictive meodeling that support informed decision-making. My work focuses on exploring datasets, identifying patterns, and communicating findings in a clear and impactful way. I enjoy approaching problems analytically, breaking them down into structured steps, and uncovering the story behind the data. Beyond data analysis, I am actively expanding towards becoming a Data Scientist, with an interest in building predictive modeling and advanced analytics.

Data Analyst| ML | Excel | Power BI | Python | SQL | Figma

Connect With Me On - [LinkedIn](https://www.linkedin.com/in/akinkunmiafod) | [Medium]() | Gmail: afodunrinbikunmi@gmail.com
