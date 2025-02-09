# Bootstrap Resampling in Python

In this notebook, we will perform bootstrap resampling to estimate confidence intervals for a sample statistic.

### Code:

```python
import numpy as np
import matplotlib.pyplot as plt

# Sample Data (Sample of 10 numbers)
data = np.array([23, 21, 19, 25, 30, 22, 18, 28, 24, 27])

# Number of Bootstrap Samples
n_iterations = 1000
n_size = len(data)

# Generate Bootstrap Samples
bootstrap_samples = np.random.choice(data, (n_iterations, n_size), replace=True)

# Calculate Mean for Each Bootstrap Sample
means = bootstrap_samples.mean(axis=1)

# Plot the distribution of bootstrap sample means
plt.hist(means, bins=30, edgecolor='black')
plt.title('Bootstrap Distribution of Means')
plt.xlabel('Mean')
plt.ylabel('Frequency')
plt.show()

# Confidence Interval (95%)
lower_bound = np.percentile(means, 2.5)
upper_bound = np.percentile(means, 97.5)
print(f"95% Confidence Interval for the Mean: ({lower_bound}, {upper_bound})")
