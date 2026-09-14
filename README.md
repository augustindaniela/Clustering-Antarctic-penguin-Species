# Clustering Antarctic Penguin Species

Using unsupervised learning (K-means) to identify penguin species groups in Antarctica, since researchers collected physical measurements but didn't record each animal's species.

*Data source: Dr. Kristen Gorman and Palmer Station, Antarctica LTER (via [Allison Horst](https://github.com/allisonhorst/penguins))*

## Context

Researchers know there are **at least 3 native species** in the region (Adelie, Chinstrap, and Gentoo), but didn't label which penguin belongs to which species. The goal is to use physical measurements to group them automatically.

## Dataset

- `penguins.csv`: culmen length and depth, flipper length, body mass, and sex — **332 penguins**

## Methodology

1. One-hot encoded the categorical `sex` column
2. **Standardized** all features with `StandardScaler` (essential for K-means, which is scale-sensitive)
3. **Elbow method:** tested k=1 to 9 clusters, tracking inertia at each step
4. Fit the final K-means model and analyzed the average profile of each cluster

## Key Findings

- The inertia curve drops sharply up through **k=4**, which was chosen as the final number of clusters
- The model found **4 clusters** (more than the 3 known species — likely because sex also affects body size within each species, creating sub-groups)
- Average profile per cluster (culmen length/depth, flipper length, body mass):

| Cluster | Culmen length (mm) | Culmen depth (mm) | Flipper (mm) | Body mass (g) |
|---|---|---|---|---|
| 0 | 43.9 | 19.1 | 194.8 | 4,007 |
| 1 | 40.2 | 17.6 | 189.0 | 3,419 |
| 2 | 49.5 | 15.7 | 221.5 | 5,485 |
| 3 | 45.6 | 14.2 | 212.7 | 4,680 |

- Clusters 2 and 3 (longer, shallower bills, larger flippers) likely correspond to the **Gentoo** species (physically the largest); clusters 0 and 1 (shorter, deeper bills) likely correspond to **Adelie**/**Chinstrap**, possibly split further by sex within species

## Tech Stack

`pandas` · `scikit-learn` (`KMeans`, `StandardScaler`) · `matplotlib`
