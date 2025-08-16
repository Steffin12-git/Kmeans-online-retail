# Online Retail — K-Means Customer Segmentation

![Python](https://img.shields.io/badge/Python-3.10%2B-3776AB?logo=python\&logoColor=white)
![scikit-learn](https://img.shields.io/badge/scikit--learn-1.x-F7931E?logo=scikitlearn\&logoColor=white)
![pandas](https://img.shields.io/badge/pandas-2.x-150458?logo=pandas\&logoColor=white)
![Matplotlib](https://img.shields.io/badge/Matplotlib-3.x-11557C?logo=matplotlib\&logoColor=white)
![Seaborn](https://img.shields.io/badge/Seaborn-0.13-4E9BCD)
![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-F37626?logo=jupyter\&logoColor=white)
![Status](https://img.shields.io/badge/Project-Complete-brightgreen)
![License](https://img.shields.io/badge/License-MIT-lightgrey)

---

> **Goal:** Use **unsupervised learning (K-Means)** on **RFM features** to uncover actionable customer segments from the **UCI Online Retail** dataset.
> **Business Impact:** Customer segmentation drives **personalized marketing**, improves **ROI**, and enhances **customer retention & engagement**.

---

## 🚀 Executive Summary

This notebook demonstrates a complete **end-to-end ML pipeline** that:

* **Cleans & standardizes** messy retail transactions
* Constructs **RFM (Recency, Frequency, Monetary)** features
* Scales features & applies **K-Means clustering**
* Determines optimal `k` via **Elbow & Silhouette** methods
* Produces **4 actionable segments + 3 outlier micro-segments**
* Visualizes clusters for business storytelling

📊 **Key Outcomes:**

* **Raw rows:** 525,461 → **Cleaned:** 406,309 (77.32% retained)
* **Unique customers:** 4,285
* **Clustered customers (after outlier removal):** 3,809
* **Optimal clusters (k):** 4
* **Actionable Segments:** Retain, Reward, Re-Engage, Nurture + Outlier cohorts (Pamper, Upsell, Delight)

---

## 📂 Dataset

* **Source:** [UCI ML Repository — Online Retail II](https://archive.ics.uci.edu/ml/datasets/Online+Retail+II)
* **Period:** 2009-12-01 → 2010-12-09
* **Countries:** 40 (UK dominates with **485,852 rows**)
* **Schema (8 cols):** `Invoice`, `StockCode`, `Description`, `Quantity`, `InvoiceDate`, `Price`, `Customer ID`, `Country`

---

## 🧹 Data Cleaning

Steps applied:

1. **Invoice filtering** → keep only 6-digit numeric invoices (`^\d{6}$`).
2. **StockCode filtering** → exclude admin/test codes (keep only SKU-like).
3. **Drop rows with missing Customer IDs.**
4. **Remove zero-priced lines** (28 rows removed).
5. **Final cleaned dataset:** 406,309 rows (77.32% of raw).

📌 **Distribution Check:**

![Distribution of RFM](./images/monetary%20value%20and%20frequency%20and%20recency%20distribution.png)

📌 **With Outliers Highlighted:**

![Boxplots with Outliers](./images/monetary%20value%20and%20frequency%20and%20recency%20distribution%20box%20plot%20with%20heavy%20outliers.png)

📌 **After Outlier Removal:**

![Boxplots after Outlier Removal](./images/monetary%20value%20and%20frequency%20and%20recency%20distribution%20box%20plot%20after%20seperating%20heavy%20outliers.png)

---

## 📊 RFM Feature Engineering

Features per customer:

* **Recency (R):** Days since last purchase
* **Frequency (F):** Number of invoices
* **Monetary (M):** Total spend

**Summary (non-outliers, 3,809 customers):**

* Recency: mean = 97d, median = 58d
* Frequency: mean = 2.86, median = 2
* Monetary: mean = 885.5, median = 588.1

---

## 🤖 Modeling

* **Algorithm:** `KMeans(n_clusters=4, random_state=42, max_iter=1000)`
* **Scaling:** StandardScaler on `[R, F, M]`
* **Model Selection:**

📌 **Elbow + Silhouette Diagnostic:**

![KMeans Inertia and Silhouette](./images/Kmean%20inertia%20and%20Silhouette%20Scores.png)

**Optimal K = 4**

---

## 🧩 Segmentation Results

### 🔑 Core Clusters

1. **Cluster 0 — Retain** (High value, recent buyers)

   * Playbook: VIP care, exclusive perks, proactive engagement.

2. **Cluster 1 — Re-Engage** (Low frequency & spend, lapsed)

   * Playbook: Win-back offers, personalized reactivation emails.

3. **Cluster 2 — Nurture** (Lowest activity, often new)

   * Playbook: Onboarding, education, low-friction deals.

4. **Cluster 3 — Reward** (Loyal, consistent buyers)

   * Playbook: Loyalty rewards, referral incentives, bundles.

📌 **Cluster Visualization (Raw):**

![3D Scatter Raw](./images/3D%20scatter%20of%20customer%20data.png)

📌 **Cluster Visualization (Scaled):**

![3D Scatter Scaled](./images/3D%20scatter%20of%20customer%20data%20after%20scaling.png)

📌 **KMeans Cluster Separation:**

![KMeans Clustered Scatter](./images/3D%20scatter%20of%20customer%20data%20seperated%20by%20Kmeans%20algorithm.png)

📌 **Violin Plots (Segment Profiles):**

![Violin Plot RFM by Cluster](./images/violin%20plot%20of%20monetary%20value%20,frequency%20and%20recency%20distribution.png)

---

### 🎯 Outlier Micro-Segments

* **Cluster −1 — Pamper** → High spenders → bespoke offers, concierge.
* **Cluster −2 — Upsell** → Frequent shoppers → subscriptions, bundles.
* **Cluster −3 — Delight** → Elite (high R + F + M) → premium tiers, surprise perks.

---

## 💼 Business Applications

* **Retention & Loyalty** → Retain & Reward cohorts
* **Reactivation Campaigns** → Target Re-Engage group
* **Acquisition Funnel** → Nurture new/dormant customers
* **Premium Strategy** → Outlier groups (Pamper, Upsell, Delight)

---

## ⚙️ Tech Stack

* **Python 3.10+**, **Jupyter Notebook**
* **pandas** → data manipulation
* **scikit-learn** → KMeans, scaling, silhouette
* **matplotlib & seaborn** → visualization
* **openpyxl** → Excel I/O

---

## 📁 Suggested Repository Structure

```
.
├── notebooks/
│   └── Kmeans_online_retail2.ipynb
├── images/                           # visual outputs
├── data/
│   └── online_retail_II.xlsx         # (ignored in git)
├── outputs/
│   ├── customer_segments_inliers.csv
│   └── customer_outliers_flagged.csv
├── README.md
└── requirements.txt
```

---

## 🌟 Highlights for Recruiters

✔️ Built a **scalable, reproducible ML pipeline** from raw retail logs

✔️ Applied **RFM analysis + K-Means** for **customer segmentation**

✔️ Delivered **business-ready insights & playbooks** tied to ROI levers

✔️ Integrated **robust data cleaning**, **outlier handling**, and **model diagnostics**

✔️ Produced **clear visualizations & segment storytelling** for stakeholders


