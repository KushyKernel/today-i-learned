# Correlation and Covariance in Python

In this notebook, we will explore the relationship between two variables using correlation and covariance.

### Code:

```python
import numpy as np
import pandas as pd
import seaborn as sns
import matplotlib.pyplot as plt

# Sample Data
np.random.seed(42)
x = np.random.normal(0, 1, 100)
y = 2 * x + np.random.normal(0, 0.5, 100)

# Covariance
cov_matrix = np.cov(x, y)
print(f"Covariance Matrix:\n{cov_matrix}")

# Correlation
correlation = np.corrcoef(x, y)[0, 1]
print(f"Pearson Correlation: {correlation}")

# Scatter Plot
plt.scatter(x, y)
plt.title('Scatter Plot')
plt.xlabel('X')
plt.ylabel('Y')
plt.show()

# Correlation Heatmap
data = pd.DataFrame({'X': x, 'Y': y})
sns.heatmap(data.corr(), annot=True, cmap='coolwarm', center=0)
plt.title('Correlation Heatmap')
plt.show()
