# Part B: Business Case Analysis

## Scenario: Promotion Effectiveness at a Fashion Retail Chain
The goal of this analysis is to understand which promotions work best across different stores and time periods. By using data and machine learning, the business can decide which promotion to apply in each store to maximize sales.

---

# B1. Problem Formulation

### (a) Machine Learning Problem Definition

* **Target Variable:**
  The target variable is **items_sold**, which represents how many products are sold in a store during a given month.

* **Input Features:**
  The model can use several types of features:

  * Store-related: `store_id`, `store_size`, `location_type`
  * Promotion-related: `promotion_type`
  * Time-related: `transaction_date`, `month`, `day_of_week`, `is_weekend`, `is_festival`
  * Market-related: `competition_density`

* **Type of Problem:**
  This is a **supervised regression problem**, since we are predicting a continuous numerical value.

* **Why this approach:**
  We already have historical data with known outcomes (items sold), so supervised learning is suitable. Since the output is numeric, regression is the correct choice.

| Component        | Description                            |
|------------------|----------------------------------------|
| Target Variable  | items_sold                             |
| ML Problem Type  | Supervised Regression                  |
| Key Features     | Store, Promotion, Time, Market factors |

---

### (b) Why Items Sold is Better Than Revenue

Revenue can be affected by pricing, discounts, and different promotion strategies, which may not accurately reflect customer demand.

On the other hand, **items sold directly shows how customers respond** to a promotion. It gives a clearer picture of whether a promotion is actually driving sales.

* **Key idea:**
  The target variable should match what the business really wants to measure. It should not be heavily influenced by external factors like pricing changes.

---

### (c) Alternative Modelling Strategy

Using a single global model for all stores may not work well because customer behavior differs by location and store type.

A better approach would be:

* Building **separate models for different store groups** (e.g., urban vs rural), or
* Including **interaction effects** between promotion type and location

This allows the model to capture differences in customer behavior and improves prediction accuracy.

---

# B2. Data and EDA Strategy

### (a) Data Integration Strategy

The data comes from multiple sources:

* Transactions
* Store information
* Promotion details
* Calendar data

These can be combined as follows:

* Join store data using `store_id`

* Join promotion data using `promotion_type`

* Join calendar data using `transaction_date`

* **Final dataset structure:**
  One row should represent **one store for one month**

* **Aggregations needed:**

  * Total `items_sold`
  * Number of transactions
  * Monthly summaries and derived features

---

### (b) Exploratory Data Analysis (EDA)

Before building the model, the following analyses would be useful:

1. **Distribution of Sales**

   * Check if `items_sold` is skewed or has outliers

2. **Sales by Promotion Type**

   * Compare how different promotions perform

3. **Sales by Store Characteristics**

   * Understand differences based on store size and location

4. **Time-based Trends**

   * Identify patterns during weekends or festivals

* **Why this matters:**
  EDA helps identify important features, detect unusual patterns, and guide feature engineering decisions.

---

### (c) Handling Promotion Imbalance

If 80% of the data has no promotion, the dataset is imbalanced.

* **Problem:**
  The model may learn to ignore promotions and focus on the majority case

* **What to do:**

  * Use balanced sampling techniques
  * Apply weights if needed
  * Ensure evaluation considers all cases
  * Include promotion-related features carefully

---

# B3. Model Evaluation and Deployment

### (a) Train-Test Split and Evaluation

Since the data is time-based, a **temporal split** should be used:

* First 80% → training

* Last 20% → testing

* **Why not random split?**
  Random splitting can mix past and future data, which leads to unrealistic results and data leakage.

* **Evaluation metrics:**

  * **RMSE** → gives more weight to large errors
  * **MAE** → easier to interpret as average error

* **Interpretation:**
  Lower values mean better predictions. MAE shows how far predictions are from actual values on average.

---

### (b) Explaining Model Predictions

Feature importance can be used to understand model decisions.

For example:

* During festivals → `is_festival` may have high impact
* In certain months → promotion type may play a bigger role

This helps explain to the marketing team why different promotions are recommended at different times.

---

### (c) Deployment Strategy

To use this model in practice:

1. **Save the trained model**

   * Use tools like joblib or pickle

2. **Prepare new monthly data**

   * Apply the same preprocessing steps

3. **Generate predictions**

   * Recommend promotions for each store

4. **Automate the process**

   * Run predictions at the start of each month

5. **Monitor performance**

   * Track RMSE/MAE over time
   * Check if accuracy drops

6. **Retrain when needed**

   * Update the model with new data periodically

---

# Conclusion

This analysis shows how machine learning can be used to improve promotion strategies in a retail setting. By building a regression model to predict items sold, the business can make more informed decisions about which promotions to apply across different stores and time periods.

The results indicate that store characteristics, promotional strategies, and time-based factors all influence sales. Using proper preprocessing, model evaluation, and feature importance analysis, the business can better understand what drives performance.

Overall, this approach helps the business apply more targeted promotions, improve sales, and make better decisions.

---*---
