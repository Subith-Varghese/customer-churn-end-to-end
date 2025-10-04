# Telecom Customer Churn Prediction – End-to-End Project

## Project Overview
This project is a complete **end-to-end data science and business intelligence solution** to predict customer churn for a telecom company.  
It combines **SQL for data engineering**, **Power BI for visualization**, and **Python (Machine Learning)** for churn prediction.

The objective is to identify customers who are likely to leave (“churn”) and provide actionable insights for retention.

---

## 🗂️ Stage 1 – Data Engineering (SQL)

**Goal:** Build clean, analysis-ready datasets.

### Steps
1. **Data Extraction**
   - Loaded raw customer and service data from SQL Server.

2. **Data Cleaning**
   - Handled nulls and duplicates.
   - Removed unused columns.
   - Created `prod_Churn` (production-ready table).

3. **Views Creation**
   - `vw_ChurnData` → Customers with status *Churned* or *Stayed*  
   - `vw_JoinData` → Newly joined customers for future predictions
---

## 📈 Stage 2 – Exploratory Analysis (Power BI)

**Goal:** Understand customer churn patterns and key drivers.
![Churn_Analysis](https://github.com/Subith-Varghese/customer-churn-end-to-end/blob/ef2cb21f6a8981daad5c7801951d15856af07de0/powerbi/Screenshot_Churn_Analysis.png)
### Key Dashboards
1. **Churn Overview**
   - Total Customers, Churn Rate, Gender Distribution
2. **Churn by Category**
   - Competitor (761), Attitude (301), Dissatisfaction (300), Price (196), Other (174)
3. **Churn by Contract**
   - Month-to-Month contracts → highest churn
4. **Internet Type**
   - Fiber Optic users → most likely to churn
5. **Payment Method**
   - Mailed Check & Bank Withdrawal → high churn
6. **Tenure vs Churn Rate**
   - Churn peaks at 6–24 months tenure
7. **State & Age Analysis**
   - Delhi & Maharashtra → top churn states  
   - Age > 65 → highest churn segment

### Insights
- Short-term contracts & manual payments are major churn drivers.  
- Fiber Optic users and middle-aged customers show high risk.  
- Loyal long-tenure customers show reduced churn.

---

## 🤖 Stage 3 – Machine Learning Model (Python)

**Goal:** Predict future churn using historical data.

### Data Preprocessing
- **Yeo-Johnson Transformation** for skew correction  
- **Outlier Capping** using IQR  
- **Label Encoding** for categorical variables  
- **Variance Threshold** for low-variance feature removal  
- **Standard Scaling** for normalization  
- **SMOTE** for class balancing

### Model: `RandomForestClassifier`
- **n_estimators:** 200  
- **Evaluation Metric:** Youden’s J threshold optimization

### Performance
| Metric | Score |
|--------|--------|
| Accuracy | 0.83 |
| Precision (Churn) | 0.67 |
| Recall (Churn) | 0.79 |
| ROC-AUC | 0.895 |
| Best Threshold (Youden’s J) | 0.39 |

### Top Features
| Rank | Feature | Importance |
|------|----------|------------|
| 1 | Contract | 0.214 |
| 2 | Total_Charges | 0.097 |
| 3 | Total_Revenue | 0.095 |
| 4 | Total_Long_Distance_Charges | 0.075 |
| 5 | Monthly_Charge | 0.073 |
| 6 | Age | 0.051 |
| 7 | Tenure_in_Months | 0.038 |
| 8 | Payment_Method | 0.037 |

### Model Assets Saved
pt.pkl # Yeo-Johnson Transformer
label_encoder.pkl # LabelEncoder
scaler.pkl # StandardScaler
rf_model.pkl # RandomForest Model
best_threshold.pkl # Optimal Threshold
top_features.pkl # Final selected features

---

## 🧠 Stage 4 – Prediction & Business Insights (Power BI)

**Goal:** Predict churn for newly joined customers (`vw_JoinData`) and visualize at-risk customers.
![Churn_Prediction](https://github.com/Subith-Varghese/customer-churn-end-to-end/blob/67c2c70ab1313e7d02565f1be4a3f3593e528498/powerbi/Screenshot_Churn_Predictions.png)

### Pipeline
1. Applied same transformations on `JoinData`
2. Generated churn probabilities
3. Applied threshold (0.39) to classify as **Stayed / Churned**
4. Saved predictions → SQL table `ChurnPredictions`
5. Visualized results in Power BI

### Predicted Churn Summary
| Metric | Count |
|--------|--------|
| Total Predicted Churners | 7 |
| Female | 4 |
| Male | 3 |

### Distribution
| Dimension | Top Categories |
|------------|----------------|
| **Contract** | 6 Month-to-Month, 1 Two-Year |
| **Payment Method** | 5 Bank Withdrawal, 2 Mailed Check |
| **Marital Status** | 5 Not Married, 2 Married |
| **State** | Delhi (2), Maharashtra (2), Andhra Pradesh (1), Haryana (1), Kerala (1) |
| **Tenure Group** | >24 Months (3), 12–18 Months (2), 6–12 Months (2) |

### Example Predicted Churners
| Customer_ID | State | Contract | Payment | Churn Probability |
|--------------|--------|-----------|-----------|--------------------|
| 44700-DEL | Delhi | Month-to-Month | Bank Withdrawal | 0.44 |
| 79777-MAH | Maharashtra | Month-to-Month | Mailed Check | 0.57 |
| 91505-DEL | Delhi | Two-Year | Bank Withdrawal | 0.39 |
| 79700-KER | Kerala | Month-to-Month | Mailed Check | 0.45 |

---

## 💡 Business Recommendations

| Area | Insight | Action |
|------|----------|--------|
| **Contract Type** | 86% churners on Month-to-Month | Offer discounts for long-term commitments |
| **Payment Method** | 71% use Bank Withdrawal | Encourage auto-pay or digital methods |
| **Customer Loyalty** | Some >24 month customers still churn | Launch loyalty / renewal bonus programs |
| **State Focus** | Delhi & Maharashtra show higher churn | Prioritize regional retention campaigns |
| **Revenue Impact** | Predicted churners are high-value | Focus retention efforts on profitable customers |

---

## 🛠️ Tools & Technologies

| Category | Tools |
|-----------|--------|
| **Data Storage & Processing** | SQL Server, Pandas |
| **Visualization** | Power BI |
| **Machine Learning** | scikit-learn, imbalanced-learn, matplotlib, seaborn |
| **Model Deployment** | SQL (via Pandas `to_sql`) |
| **Libraries Used** | numpy, pandas, sklearn, joblib, seaborn, matplotlib |

---

## 📘 Project Deliverables

| File / Output | Description |
|----------------|-------------|
| `prod_Churn` (SQL) | Cleaned production dataset |
| `Churn Analysis.pbix` | Power BI analysis of historical churn |
| `churn_model.ipynb` | Python ML pipeline |
| `ChurnPredictions` (SQL) | Predicted churners table |
| `Churn Prediction Dashboard.pbix` | Power BI dashboard for predicted churn |

---

## 🧾 Final Results Summary

✅ **Full churn lifecycle implemented**  
✅ **0.895 ROC-AUC Random Forest model**  
✅ **Automated prediction back to SQL**  
✅ **Insightful Power BI dashboards for decision-making**

