# BTT-JPMC-1
**Break Through Tech Relationship Analysis Tool**

Using S&P 500 stock price data, our project explores how uncovering inter-company relationships through clustering can enhance financial prediction models—particularly stock price forecasting. By leveraging XGBoost and hierarchical clustering, we aim to boost predictive accuracy for better investment insights.


##  Exploratory Data Analysis

- Scraped daily closing prices of S&P 500 companies from **Yahoo Finance** between **01/03/2022 and 12/31/2022**.
- Converted data into **daily return percentages** to better reflect relative movement rather than raw price.
- Constructed a **correlation matrix** using daily returns to understand co-movements between stocks.
- Identified strong sectoral groupings (e.g., Energy, Financials) through patterns in return behavior.

---

##  Data Cleaning

- Dropped weeks with market closures (resulting in missing data).
- Final dataset includes **41 usable weeks** per company with valid return data.
- Removed incomplete or anomalous entries to ensure consistent input for both clustering and modeling.

---

##  Clustering

- Applied **Hierarchical Clustering** using **Ward linkage** and **absolute correlation distance** (`1 - |r|`) to measure similarity.
- Constructed a **dendrogram** and chose a cutoff that yielded **3 distinct clusters**.
- Evaluated clustering quality using **silhouette scores** (achieved score: `0.2405`).
- Final distribution: `[392, 27, 79]` companies in each cluster respectively.

---

##  Model Creation 

- Built two sets of **XGBoost regression models**:
  1. **Baseline Model** – trained without any clustering data.
  2. **Cluster-Enhanced Model** – trained separately on each cluster to capture intra-group patterns.

- Input Features: Daily returns for 4 days (Mon–Thu) → Predict Friday return (Day 5).
- Each week per company forms a single training sample (41 samples per company).

---

##  Hyperparameter Tuning

Used **grid search** for each model with the following tuning parameters:

- `max_depth`: [2, 3, 5, 7, 8, 10]
- `n_estimators`: [100, 200, 300, 400]
- `learning_rate`: [0.001, 0.005, 0.01, 0.05, 0.1]

---
## Performance
Evaluation Metrics: MSE, RMSE, and MAE.

Cluster-specific models significantly outperformed the baseline in terms of error reduction.

Visualizations showed improvement in prediction consistency after integrating cluster insights.

---
## Next Steps
Outlier handling: Detect and evaluate companies or time periods with unusual behavior.

Expand features: Include sentiment analysis from news and social media (Reddit, Twitter).

Build an interactive dashboard to visualize company clusters and relationships.

---

