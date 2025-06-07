# SeCo Framework for Choosing *k* in K-Means

This markdown explains the SeCo (Separation–Concordance) framework, used to help determine the optimal number of clusters (*k*) in K-Means through parallelised sampling and stability evaluation.

## Summary

| Concept         | What it means                                                            |
|-----------------|--------------------------------------------------------------------------|
| **Separation**  | Between-cluster sum-of-squares (higher ⇒ cleaner splits)                 |
| **Concordance** | Median Cramer’s *V* across the best 50 runs (higher ⇒ stable solutions)  |
| **SeCo Plot**   | Scatter of Concordance vs Separation — pick the top-right zone           |

## Prerequisites

```bash
pip install numpy pandas scikit-learn scipy joblib matplotlib

```


### Code:

```python 
import numpy as np
import pandas as pd
from sklearn.cluster import KMeans
from sklearn.metrics import confusion_matrix
from scipy.stats import chi2_contingency
from joblib import Parallel, delayed
import matplotlib.pyplot as plt

# Load dataset
df = pd.read_csv(r"C:/Users/tifek/Documents/Data Science/scaled.csv")
data = df.values

m, n = data.shape
k_range = list(range(2, 11))
kmsamples = 500
topsep = 50

# 1) Parallel KMeans sampling
def cluster_one(i, j, k):
    km = KMeans(n_clusters=k, init="random", n_init=1)
    return i, j, km.fit_predict(data)

results = Parallel(n_jobs=-1, verbose=5)(
    delayed(cluster_one)(i, j, k_range[j])
    for i in range(kmsamples)
    for j in range(len(k_range))
)

labels = np.zeros((m, kmsamples, len(k_range)), dtype=int)
for i, j, lab in results:
    labels[:, i, j] = lab

# 2) Compute Separation
SSQ0 = np.sum((data - data.mean(axis=0))**2)

def compute_ssq(i, j):
    SSQ_within = 0
    for cid in np.unique(labels[:, i, j]):
        mask = labels[:, i, j] == cid
        centroid = data[mask].mean(axis=0)
        SSQ_within += np.sum((data[mask] - centroid)**2)
    return i, j, SSQ0 - SSQ_within

ssq_results = Parallel(n_jobs=-1, verbose=5)(
    delayed(compute_ssq)(i, j)
    for i in range(kmsamples)
    for j in range(len(k_range))
)

SSQdata = np.zeros((kmsamples, len(k_range)))
for i, j, ssq in ssq_results:
    SSQdata[i, j] = ssq

# 3) Top-50 by Separation
order = np.argsort(SSQdata, axis=0)[::-1]
best_idx = order[:topsep, :]

bestSSQsolutions = np.zeros((m, topsep, len(k_range)), dtype=int)
SSQdatabest = np.zeros((topsep, len(k_range)))
for j in range(len(k_range)):
    bestSSQsolutions[:, :, j] = labels[:, best_idx[:, j], j]
    SSQdatabest[:, j] = SSQdata[best_idx[:, j], j]

# 4) Median Cramer's V for Concordance
def cramer_v(x, y):
    cm = confusion_matrix(x, y)
    chi2, _, _, _ = chi2_contingency(cm, correction=False)
    n = cm.sum()
    phi2 = chi2 / n
    r, c = cm.shape
    return np.sqrt(phi2 / min(r - 1, c - 1))

cvdata = np.zeros((topsep, len(k_range)))
for j in range(len(k_range)):
    for i in range(topsep):
        x = bestSSQsolutions[:, i, j]
        vals = [cramer_v(x, bestSSQsolutions[:, h, j]) for h in range(topsep) if h != i]
        cvdata[i, j] = np.median(vals)

# 5) SeCo Plot
markers = "ox*sdv+^<>ph"
plt.figure(figsize=(8, 6))
for idx, k in enumerate(k_range):
    plt.scatter(cvdata[:, idx], SSQdatabest[:, idx],
                label=f"k={k}",
                marker=markers[idx % len(markers)],
                s=50, alpha=0.7)
plt.xlabel("Concordance")
plt.ylabel("Separation")
plt.title("SeCo Framework")
plt.grid(True)
plt.legend()
plt.tight_layout()
plt.show()
```

![SeCo Plot](/Python/ML/images/SeCo.png)


