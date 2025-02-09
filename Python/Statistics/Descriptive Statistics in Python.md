# Descriptive Statistics in Python

This notebook demonstrates visualizations like histograms and box plots, as well as computing basic summary statistics.

### Code:

```python
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns

# Sample Data
data = np.random.normal(0, 1, 1000)

# Histogram
plt.hist(data, bins=30, edgecolor='black')
plt.title('Histogram')
plt.xlabel('Value')
plt.ylabel('Frequency')
plt.show()

# Box Plot
sns.boxplot(data=data)
plt.title('Box Plot')
plt.show()

# Summary Statistics
mean = np.mean(data)
median = np.median(data)
std_dev = np.std(data)
print(f"Mean: {mean}, Median: {median}, Standard Deviation: {std_dev}")
