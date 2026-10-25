# Customer Churn Analysis
 
Exploratory data analysis to identify the factors most strongly associated with customer churn, with actionable retention recommendations.
 
## Objective
 
Find out which customer attributes (contract type, payment method, tenure, internet service, demographics) drive churn, and translate them into retention strategies.
 
## Project Structure
 
```
.
├── churn.csv/                # Raw dataset (update filename as needed)
├──── churn_analysis.ipynb     # EDA + visualizations                
├── requirements.txt
└── README.md
```
 
## Setup
 
```bash
git clone <your-repo-url>
cd <repo-name>
python -m venv .venv && source .venv/bin/activate   # Windows: .venv\Scripts\activate
pip install -r requirements.txt
jupyter notebook notebooks/churn_analysis.ipynb
```
 
`requirements.txt`
 
```
pandas
numpy
matplotlib
seaborn
jupyter
```
 
## Methodology
 
1. **Data cleaning**: handle missing values, fix dtypes, standardize the target (`Churn` → 0/1).
2. **Segmentation**: group by `Contract`, `PaymentMethod`, `tenure` bins, `InternetService`, `SeniorCitizen`.
3. **Churn rate**: `churn_rate = churned_customers / total_customers_in_segment * 100`.
4. **Visualization**: bar plots (categorical segments) and line graphs (tenure trend).
5. **Insight and recommendation synthesis**.
```python
# Churn rate (%) per segment
churn_rate = (
    df.groupby("Contract")["Churn"]
      .mean()
      .mul(100)
      .round(1)
      .sort_values(ascending=False)
)
```
 
## Key Findings
 
| Factor | Segment | Churn Rate |
|---|---|---|
| Contract | Month-to-month | ~42% |
| Contract | One year | ~11% |
| Contract | Two year | ~3% |
| Payment method | Electronic check | ~45% |
| Payment method | Credit card / bank transfer / mailed check | ~15-18% |
| Tenure | < 1 year | ~50% <!-- VERIFY against notebook --> |
| Tenure | 1-3 years | ~35% <!-- VERIFY against notebook --> |
| Tenure | > 3 years | ~15% <!-- VERIFY against notebook --> |
| Internet service | Fiber optic | ~30% <!-- VERIFY against notebook --> |
| Internet service | DSL | ~20% <!-- VERIFY against notebook --> |
| Demographics | Senior citizens | ~41% |
| Demographics | Non-senior | ~26% <!-- VERIFY against notebook --> |
 
### Takeaways
 
- **Contract type**: month-to-month customers churn far more than yearly or two-year customers; long-term commitment is a strong retention lever.
- **Payment method**: electronic check users churn roughly 3x more than users of automatic or traditional methods.
- **Tenure**: churn is highest in the first year and declines steadily as tenure grows, so early engagement is critical.
- **Internet service**: fiber optic customers churn more than DSL customers, possibly due to competition or service-quality issues.
- **Seniors**: senior citizens churn notably more than non-seniors.
## Recommendations
 
1. **Promote long-term contracts**: offer discounts or perks for 1-2 year plans.
2. **Shift payment behavior**: incentivize migration from electronic check to auto-pay (card / bank transfer).
3. **Early-tenure engagement**: onboarding flows, check-ins, and loyalty offers in the first 12 months.
4. **Fiber service quality**: investigate satisfaction, speed, and reliability issues.
5. **Senior retention programs**: dedicated support and tailored plans.
## Limitations
 
- Findings are **associations, not causal claims**.
- Single-factor segmentation; interactions (e.g., month-to-month + electronic check) are not modeled.
- Class imbalance may affect any downstream predictive modeling.
## Next Steps
 
- Multivariate analysis and feature importance (Logistic Regression, Random Forest, XGBoost).
- Churn prediction model with proper evaluation (ROC-AUC, PR-AUC, recall on churners).
- Survival analysis on tenure.
- A/B test the proposed retention interventions.
## Author
 
Neelesh
 
