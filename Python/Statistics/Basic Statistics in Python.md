# Basic Statistics in Python

In this notebook, we will cover foundational statistics concepts like mean, median, mode, variance, and standard deviation.

### Code:

```python
import numpy as np
import scipy.stats as stats

# Sample Data
data = [12, 15, 18, 22, 25, 29, 33, 38, 40, 45]

# Mean
mean = np.mean(data)
print(f"Mean: {mean}")

# Median
median = np.median(data)
print(f"Median: {median}")

# Mode
mode = stats.mode(data)
print(f"Mode: {mode.mode[0]}")

# Variance
variance = np.var(data)
print(f"Variance: {variance}")

# Standard Deviation
std_dev = np.std(data)
print(f"Standard Deviation: {std_dev}")