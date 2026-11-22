# MSCS 634 — Advanced Data Mining for Data-Driven Insights and Predictive Modeling

**Student:** Ruchitha Musku  
**Dataset:** IBM Telco Customer Churn  
**Final deliverable:** Final Insights, Recommendations, and Presentation

## Project overview

This project examines customer churn and revenue patterns using the IBM Telco Customer Churn dataset (7,043 customers, 21 original attributes). Across four deliverables, the work covers data quality, exploratory analysis, feature engineering, regression, classification, clustering, and association rule mining. The overall goal is to identify interpretable, actionable strategies to improve customer retention.

## Dataset and motivation

The dataset includes demographics, tenure, contract information, billing methods, internet and phone service subscriptions, monthly and total charges, and a churn outcome. It is sufficiently large and varied to support the required supervised and unsupervised methods. The publicly shared dataset represents a fictional telecom business; findings should not be treated as established causal effects in a real customer population.

## Project workflow

### Deliverable 1 — Data preparation and EDA

- Inspected 7,043 records and corrected 11 blank `TotalCharges` values. All 11 customers had zero tenure, so their total charges were set to zero.
- Standardized categorical values and verified duplicated-looking service categories against parent service fields.
- Checked customer ID uniqueness, outliers, numeric ranges, and cross-field consistency.
- Explored churn rates by contract, tenure, internet service, payment type, and support add-ons.
- Found overall churn of **26.5%**. Month-to-month customers had a reported churn rate of **42.7%**, versus **2.8%** for two-year contracts. These are associations, not proof that contract changes cause improved retention.

### Deliverable 2 — Regression and feature engineering

- Target: `TotalCharges` (revenue); deliberately excluded `MonthlyCharges` and churn status to reduce target leakage.
- Engineered tenure × service interactions and summary service/account features.
- Compared baseline and engineered linear regression, Ridge, Lasso, and Random Forest with train/test evaluation and cross-validation.
- **Engineered Lasso** was the reported top performer: **test R² = 0.9986; RMSE = $85.00; MAE = $54.20**. This high performance is consistent with the strong arithmetic structure of cumulative charges and should not be generalized to customer-behavior prediction.
- A supplementary tenure regression achieved a more modest **test R² = 0.670**.

### Deliverable 3 — Classification, clustering, and association rules

- Tested Decision Tree, k-NN, Gaussian Naïve Bayes, SVM, and Logistic Regression for customer churn.
- The **tuned Decision Tree** delivered **F1 = 0.621, recall = 0.783, ROC-AUC = 0.816**; Logistic Regression achieved the highest reported ROC-AUC (**0.841**).
- K-Means segmentation identified four customer groups. Two higher-risk groups accounted for about **91.5% of observed churners**.
- Apriori and FP-Growth surfaced relationships between customer characteristics and churn. One rule, **{Fiber optic, PaperlessBilling, tenure ≤ 12 months} → Churn**, had **72.3% confidence** and **2.72 lift**.

## Consolidated findings

| Analysis | Result | Business interpretation |
|---|---|---|
| EDA | 26.5% overall churn | Retention represents a material customer-management challenge |
| EDA | 42.7% churn in month-to-month customers | Flexible-contract customers merit closer investigation |
| Regression | Lasso test R² 0.9986, RMSE $85.00 | Service and tenure information can closely reconstruct cumulative billing in this dataset |
| Classification | Tuned tree F1 0.621, recall 0.783 | A compact rules-based churn screen may support outreach |
| Classification | Logistic regression ROC-AUC 0.841 | Risk scores can prioritize outreach when resources are limited |
| Clustering | Two segments account for ~91.5% of churners | Target interventions to high-risk segments rather than everyone |
| Rules | Newer fiber customers appear in high-lift churn rules | Investigate first-year onboarding and service experience |

## Practical recommendations

1. **Strengthen first-year onboarding:** prioritize proactive support for newly subscribed fiber-optic and month-to-month customers; evaluate outcomes using controlled experiments.
2. **Test voluntary contract incentives:** offer relevant upgrades rather than assuming contract length alone reduces churn.
3. **Offer support-service trials:** evaluate whether relevant security/technical-support bundles improve customer experience without undue pressure.
4. **Offer payment-method choice:** test discounts for automatic payments while preserving access for customers who cannot use them.
5. **Pilot risk-based outreach:** compare tuned-tree rule lists against logistic-regression ranking, monitoring response rates and customer experience.
6. **Monitor business outcomes:** evaluate churn reduction, retention cost, response rate, customer satisfaction, and subgroup differences.

## Ethical considerations and limitations

- **Privacy:** use minimal customer-level data, remove direct identifiers from analytic views, restrict access, and avoid publishing identifiable records from real deployments.
- **Fairness:** older age and household variables may correlate with churn; correlation should not become a basis for exclusion or discriminatory pricing. Evaluate error rates and intervention benefits across relevant groups.
- **Bias and representativeness:** this fictional sample may not represent other telecom businesses or current markets; externally validate before operational use.
- **Causality:** contracts, add-ons, and payment methods are associated with churn, but the analyses do not demonstrate that changing these factors causes retention.
- **Transparency:** use interpretable rules, provide human review and customer choice, and do not use predictions to deny service.
- **Model evaluation:** a 26.5% positive class motivates attention to recall, F1, ROC-AUC, calibration, and false positives—not accuracy alone.

**Note:** The above are ethical recommendations; do not interpret them as proof that all safeguards were already implemented in the original experiments.

## Project files

This starter repository is **not yet a complete submission**. Copy or combine the verified source files from Deliverables 1–3 as follows:


## Reproducibility

After merging the original notebooks and data, document Python version and package dependencies, install `requirements.txt`, and run all notebook cells from a clean environment. Confirm that all required plots and numeric results reproduce. Relative paths should resolve from the repository root.

## Video presentation

**Recording (5–7 minutes):** [Add accessible ScreenPal/other recording link here after recording].

The recording should explain dataset choice, cleaning and EDA, feature engineering and models, key results, recommendations, ethics and limitations, and future improvements.

## Source deliverables

- [Deliverable 1 — Data Collection, Cleaning, and Exploration](https://github.com/rmusku61699/MSCS_634_ProjectDeliverable_1)
- [Deliverable 2 — Regression Modeling and Performance Evaluation](https://github.com/rmusku61699/MSCS_634_ProjectDeliverable_2)
- [Deliverable 3 — Classification, Clustering, and Pattern Mining](https://github.com/rmusku61699/MSCS_634_ProjectDeliverable_3)

## References

- IBM. *Telco Customer Churn sample dataset*. https://github.com/IBM/telco-customer-churn-on-icp4d
- Pedregosa, F., et al. (2011). Scikit-learn: Machine learning in Python. *Journal of Machine Learning Research, 12*, 2825–2830.
- Original course project notebooks and README files (links above).
