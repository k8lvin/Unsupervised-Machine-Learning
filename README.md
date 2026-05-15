# Unsupervised Machine Learning: Customer Segmentation with K-Means and Hierarchical Clustering

This repository contains a practical, notebook-based introduction to **unsupervised learning** for customer segmentation. The project demonstrates how to:

- generate a synthetic customer dataset,
- preprocess and scale features,
- choose the number of clusters with the elbow method,
- build and interpret clusters with **K-Means**,
- compare results with **Agglomerative (Hierarchical) Clustering**, and
- visualize clusters and cluster profiles.

The full workflow lives in:

- `unsupervised_learning.ipynb`

---

## Table of Contents

1. [Project Overview](#project-overview)
2. [Learning Objectives](#learning-objectives)
3. [Repository Structure](#repository-structure)
4. [Dataset Description](#dataset-description)
5. [Methods Used](#methods-used)
6. [Notebook Walkthrough](#notebook-walkthrough)
7. [How to Run](#how-to-run)
8. [Expected Outputs](#expected-outputs)
9. [Interpretation Tips](#interpretation-tips)
10. [Limitations and Next Steps](#limitations-and-next-steps)
11. [Tech Stack](#tech-stack)

---

## Project Overview

In many real-world business problems, you have rich customer behavior data but no predefined labels (for example, no "high value" or "at-risk" tag). This is a classic **unsupervised learning** setting.

This project uses clustering to discover natural groups of customers based on behavior features, including:

- annual spend,
- visit frequency, and
- average basket size.

The notebook first applies **K-Means clustering** and then contrasts it with **hierarchical clustering** to show how different unsupervised techniques can uncover similar or complementary structure in the same data.

---

## Learning Objectives

By completing this notebook, you should be able to:

- Explain the difference between supervised and unsupervised learning.
- Apply feature scaling before distance-based clustering.
- Use the **elbow method** to estimate a suitable value of `K`.
- Fit and evaluate a K-Means model.
- Build and interpret a hierarchical clustering dendrogram.
- Compare segmentation outputs from K-Means and Agglomerative clustering.
- Communicate clustering results in a business-friendly way.

---

## Repository Structure

```text
.
├── README.md
└── unsupervised_learning.ipynb
```

---

## Dataset Description

The notebook creates a synthetic dataset of approximately 300 customers with behavior-like attributes.

### Features

- **annual_spend**: Total yearly spending (numeric).
- **visit_frequency**: Number of visits/interactions over a period (numeric).
- **avg_basket_size**: Average basket/cart value (numeric).

The data is intentionally generated from multiple underlying patterns so clustering algorithms can recover meaningful segments.

---

## Methods Used

### 1) Standardization

Because clustering methods are distance-based, feature scaling is essential. The notebook uses `StandardScaler` so all features are centered and comparable in scale.

### 2) K-Means Clustering

K-Means partitions points into `K` clusters by minimizing within-cluster variance.

Workflow in notebook:

1. Try values of `K` from 1 to 10.
2. Collect inertia (within-cluster sum of squares).
3. Plot elbow curve.
4. Select `K` (set to 4 in this notebook).
5. Fit final K-Means model and assign cluster labels.
6. Compute segment-level profiles.

### 3) Elbow Method

The elbow plot helps identify where additional clusters produce diminishing returns in inertia reduction.

### 4) Hierarchical (Agglomerative) Clustering

Agglomerative clustering starts with one point per cluster and repeatedly merges the closest clusters according to a linkage criterion (Ward linkage is used in this notebook).

Workflow in notebook:

1. Sample subset for dendrogram readability.
2. Build linkage matrix.
3. Plot dendrogram.
4. Choose a cut level / number of clusters.
5. Fit `AgglomerativeClustering` to the full scaled dataset.
6. Compare profiles against K-Means segments.

---

## Notebook Walkthrough

### Section A: Conceptual foundation

- What unsupervised learning means
- Supervised vs unsupervised comparison
- Intro to K-Means

### Section B: Data generation and inspection

- Synthetic data creation with multiple customer types
- Shape/info/head/summary checks

### Section C: Preprocessing and K-Means

- Feature scaling
- Elbow curve creation
- Final K-Means fit with 4 clusters
- Segment naming and scatter visualization

### Section D: Hierarchical clustering

- Dendrogram construction using Ward linkage
- Agglomerative clustering with 4 clusters
- Profile and visual comparison with K-Means

---

## How to Run

### Option 1: Jupyter Notebook (recommended)

1. Clone this repository.
2. Create and activate a Python environment.
3. Install dependencies.
4. Launch Jupyter and open `unsupervised_learning.ipynb`.
5. Run cells top to bottom.

### Example setup

```bash
git clone <your-repo-url>
cd Unsupervised-Machine-Learning
python -m venv .venv
source .venv/bin/activate   # On Windows: .venv\Scripts\activate
pip install numpy pandas matplotlib scikit-learn scipy jupyter
jupyter notebook
```

---

## Expected Outputs

When you run the notebook, you should see:

- A synthetic customer dataframe preview.
- Elbow curve for selecting `K`.
- K-Means cluster assignments.
- Cluster summary table (mean behavioral values by cluster).
- Dendrogram for hierarchical clustering.
- Agglomerative cluster assignments.
- Side-by-side visual comparison of K-Means vs hierarchical segments.

---

## Interpretation Tips

- Clusters are **relative groupings**, not absolute truth.
- Always profile clusters with business metrics to assign meaningful labels.
- Compare multiple clustering methods to test robustness.
- Segment quality can be sensitive to scaling, feature engineering, and random seed.

---

## Limitations and Next Steps

### Current limitations

- Uses synthetic (not real) customer data.
- No formal cluster validation metrics (e.g., silhouette score) included yet.
- K-Means assumes spherical clusters and equal variance tendencies.

### Suggested extensions

- Add **Silhouette Score**, **Calinski-Harabasz**, and **Davies-Bouldin** metrics.
- Test alternative models such as **DBSCAN** or **Gaussian Mixture Models**.
- Run sensitivity analysis for different `K`, random seeds, and feature sets.
- Add feature engineering (recency, tenure, discount usage, etc.).
- Export reusable segmentation pipeline as Python script/package.

---

## Tech Stack

- **Python**
- **NumPy**
- **Pandas**
- **Matplotlib**
- **scikit-learn**
- **SciPy**
- **Jupyter Notebook**

---

If this project helps you, consider extending it with real-world data and reproducible evaluation metrics to turn this into a production-ready segmentation baseline.
