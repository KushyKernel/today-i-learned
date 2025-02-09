# Feature Selection in Python

This notebook demonstrates how to select the most important features using statistical tests like **f_regression**.

### Code:

```python
import numpy as np
import pandas as pd
from sklearn.datasets import make_regression
from sklearn.feature_selection import SelectKBest, f_regression

# Generate Sample Data (regression problem)
X, y = make_regression(n_samples=200, n_features=10, noise=0.1, random_state=42)

# Perform Feature Selection using SelectKBest (choose top 5 features)
selector = SelectKBest(score_func=f_regression, k=5)
X_selected = selector.fit_transform(X, y)

# Display selected features and their scores
selected_features = selector.get_support(indices=True)
feature_scores = selector.scores_

print(f"Selected Features: {selected_features}")
print(f"Feature Scores: {feature_scores[selected_features]}")
