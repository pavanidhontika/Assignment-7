# Assignment 7 — Customer Segmentation using K-Means Clustering and PCA

## Objective
Segment mall customers into distinct groups based on age, gender, annual income, and spending
behavior using K-Means clustering, and visualize the resulting clusters in two dimensions using
Principal Component Analysis (PCA).

## Dataset
Mall Customer Segmentation Data (Kaggle):
https://www.kaggle.com/datasets/vjchoudhary7/customersegmentation-tutorial-in-python

> The dataset is **not** included in this repository (per the assignment's licensing
> instructions). Download it from the Kaggle link above and place `Mall_Customers.csv` in the
> project folder, or let the notebook download it automatically via `kagglehub` (requires a
> Kaggle API token at `~/.kaggle/kaggle.json`).

## Libraries Used
- `pandas` — data loading and wrangling
- `scikit-learn` — `StandardScaler`, `LabelEncoder`, `KMeans`, `PCA`
- `matplotlib` — Elbow curve and cluster visualizations
- `kagglehub` — optional automated dataset download

## Methodology
1. **Data Understanding:** Loaded the dataset, separated numerical (`Age`, `Annual Income`,
   `Spending Score`) from categorical (`Genre`/Gender) features, and reviewed summary statistics.
2. **Preprocessing:** Checked for missing values (none found), dropped the non-predictive
   `CustomerID` column, label-encoded gender, and standardized all features with `StandardScaler`.
3. **Model Development:** Used the Elbow Method across K = 1–10 to identify the optimal cluster
   count, trained K-Means with the chosen K, assigned cluster labels, and reduced the standardized
   features to 2 principal components with PCA.
4. **Visualization & Evaluation:** Plotted the elbow curve, a raw-feature scatter plot (Income vs.
   Spending Score) colored by cluster, and a PCA-projected scatter plot colored by cluster, then
   profiled each cluster's average characteristics.

## Results
The Elbow Method points to **K = 5** as the optimal number of clusters — the inertia curve bends
sharply there and flattens afterward. The five resulting segments correspond to well-known retail
customer archetypes:

| Cluster | Profile |
|---|---|
| High income, high spending | Prime marketing target — premium offers, loyalty perks |
| High income, low spending | Price-sensitive despite means — needs a different pitch (value framing) |
| Mid income, mid spending | "Standard" customers — largest stable segment |
| Low income, high spending | Impulsive spenders — respond well to promotions/discounts |
| Older, mid income, low-mid spending | More conservative buying behavior |

The 2 principal components together capture roughly **60%** of the total variance, which is
enough to visually confirm that the clusters found by K-Means are genuinely well-separated rather
than an artifact of the 2D projection.

**Observations:**
1. The elbow curve flattens noticeably at K = 5, matching the dataset's well-known 5-segment
   structure.
2. PCA compresses the 4-dimensional feature space into 2 components capturing the directions of
   greatest variance, making it possible to visually validate cluster separation that can't be
   seen directly in 4D.
3. Clusters separate almost entirely along the income/spending axes; age and gender contribute far
   less to the split.
4. Each segment maps to a distinct, actionable customer archetype for targeted marketing.

## Conclusion
This project applied K-Means clustering to segment mall customers using age, gender, annual
income, and spending score, selecting the optimal number of clusters (K = 5) via the Elbow Method
and visualizing the results with PCA. The five segments map cleanly onto recognizable customer
archetypes — from high-income big spenders to budget-conscious shoppers — which a mall's marketing
team could use to target promotions, loyalty programs, or product placement differently for each
group rather than treating all customers identically. This kind of segmentation directly supports
business applications like personalized marketing campaigns, inventory planning by store section,
and identifying high-value customers for retention efforts. A limitation of K-Means is that it
requires the number of clusters to be chosen in advance and assumes roughly spherical, similarly
sized clusters, which can misrepresent segments that are irregularly shaped or overlapping. PCA, on
the other hand, offers the advantage of reducing dimensionality while preserving as much variance
as possible, making it possible to visually validate cluster quality even when the original feature
space cannot be plotted directly.
