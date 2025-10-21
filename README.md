# Telecom Customer Churn: A Deep-Dive Analysis

This project performs a comprehensive exploratory data analysis (EDA) on the "Telco Customer Churn" dataset. The goal is to identify the key drivers of customer churn, quantify their impact, and develop a profile for high-risk customers.

The analysis moves from high-level demographic and service-level insights to a deep dive into the financial and contractual factors that have the strongest influence on customer loyalty.

##  Data Source

The analysis uses the "Telco Customer Churn" dataset, widely available on Kaggle. This dataset includes customer information related to:
* **Demographics:** `gender`, `SeniorCitizen`, `Partner`, `Dependents`
* **Account Info:** `tenure`, `Contract`, `PaymentMethod`, `PaperlessBilling`, `MonthlyCharges`, `TotalCharges`
* **Services:** `PhoneService`, `MultipleLines`, `InternetService`, `OnlineSecurity`, `OnlineBackup`, `DeviceProtection`, `TechSupport`, `StreamingTV`, `StreamingMovies`
* **Target Variable:** `Churn` (Yes/No)

##  Key Questions Answered

1.  Which customer demographics are most correlated with churn?
2.  How do `Contract` type and customer `tenure` (loyalty) interact to predict retention?
3.  What is the impact of specific internet and phone services on the likelihood of churning?
4.  Which additional services (e.g., `TechSupport`, `OnlineSecurity`) are most effective at reducing churn?
5.  How do `PaymentMethod`, `PaperlessBilling`, and monthly/total charges relate to churn behavior?
6.  What is the financial cost of churn?
7.  What are the top-ranked drivers of churn overall?
8.  What does a "high-risk" customer profile look like?

## 🧪 Methodology

The analysis is conducted using Python and relies heavily on `pandas` for data manipulation, `matplotlib` and `seaborn` for visualization, and `scipy.stats` for statistical validation.

1.  **Exploratory Data Analysis (EDA):** Churn rates are calculated for various customer segments by grouping the data by different categorical features.
2.  **Statistical Testing:**
    * **Chi-Square Test of Independence:** Used to determine if a statistically significant relationship exists between categorical variables (e.g., `Contract`, `InternetService`) and the `Churn` variable. A low p-value (e.g., `< 0.0001`) confirms the relationship is not due to random chance.
    * **Mann-Whitney U Test:** Used to compare the distributions of numerical features (e.g., `tenure`, `MonthlyCharges`) between the churned and retained customer groups. This is a non-parametric test, ideal for data that isn't normally distributed.
    * **Odds Ratio:** Calculated to quantify the increased (or decreased) odds of churning based on a specific feature (e.g., `PaperlessBilling`).
3.  **Feature Importance:** A composite ranking was built using multiple methods (Chi-Square, Random Forest Importance, Mutual Information) to identify the most powerful and reliable predictors of churn.
4.  **Customer Segmentation:** Rule-based segments were created based on the top churn drivers to build actionable profiles of high-risk customers.

##  Key Findings & Insights

### 1. Contract & Tenure: The Pillars of Loyalty

* **Contract is the #1 Driver:** Customers on **Month-to-Month** contracts are extremely high-risk, with a **42.7% churn rate**. In contrast, `One Year` (11.3%) and `Two Year` (2.9%) contracts are very "sticky."
* **Tenure is the "Danger Zone":** The first year is the most critical period.
    * The median tenure for a churned customer is only **10 months** (vs. 38 months for a retained customer).
    * Customers in their first 6 months have a **53.3% churn rate**.
    * **55.5% of all churned customers leave within the first 12 months.**

### 2. Financial Factors: How They Pay Matters

* **Payment Method:** `Electronic check` is a massive red flag. Customers using it churn at a rate of **45.3%**, far higher than `Mailed check` (19.2%) or automatic payments (15-16%).
* **Paperless Billing:** Customers with paperless billing are **2.6 times more likely to churn** (33.6% churn rate) than those with paper bills (16.4%).
* **Charges:**
    * **High Monthly Charges:** Churning customers pay more per month on average ($74.44) than retained customers ($61.31).
    * **Low Total Charges:** Churning customers have significantly lower lifetime charges, confirming they leave before their value can be realized.
    * **Insight:** The most dangerous combination is a **new customer hit with a high monthly bill**.

### 3. Services: Bundling for Retention

* **Internet Service:** `Fiber Optic` service has a high churn rate (**41.9%**), much higher than `DSL` (19.0%). This suggests price sensitivity or service instability.
* **Critical Add-ons:** The most valuable "savers" are support-based services.
    * Customers with **No Tech Support** churn at 41.6% (vs. 15.2% for those with it).
    * Customers with **No Online Security** churn at 41.8% (vs. 14.6% for those with it).
    * Having `Tech Support` or `Online Security` **reduces the risk of churning by ~64-65%**.
* **Minor Factors:** `Gender` has no statistical impact on churn. `PhoneService` type has a very minor, though statistically significant, effect.

### 4. Quantifying the Cost of Churn

This analysis estimates a significant financial drain from the 1,869 customers who churned:
* **Lost Monthly Revenue:** **$139,130.85**
* **Wasted Acquisition Cost (Est.):** **$560,700.00**
* **Total Immediate Cost:** **$699,830.85**

##  Profile: The High-Risk Customer

Based on the analysis, we can build actionable segments of customers who are most likely to leave.

* **Segment 1: "New_Echeck" (63.1% Churn Rate)**
    * **Contract:** Month-to-month
    * **Tenure:** 12 months or less
    * **Payment:** Electronic check

* **Segment 2: "Premium_NoSupport" (60.6% Churn Rate)**
    * **Contract:** Month-to-month
    * **Charges:** High (above median)
    * **Services:** No `TechSupport` AND No `OnlineSecurity`

##  Tools & Libraries Used

* **Python 3.x**
* **pandas:** For data manipulation and aggregation.
* **numpy:** For numerical operations.
* **matplotlib & seaborn:** For data visualization.
* **scipy.stats:** For Chi-Square, Mann-Whitney U, and confidence interval calculations.
* **sklearn (scikit-learn):** For feature importance modeling (Random Forest, Mutual Information).

---
