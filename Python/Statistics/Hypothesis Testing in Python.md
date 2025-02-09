# Hypothesis Testing in Python

This notebook demonstrates hypothesis testing techniques such as t-tests and chi-square tests.

### Code:

```python
import numpy as np
from scipy import stats

# Sample Data
group1 = np.array([22, 24, 27, 29, 31, 35, 37])
group2 = np.array([18, 21, 25, 27, 30, 33, 36])

# One-Sample t-Test (Testing if group1 mean is 30)
t_stat, p_value = stats.ttest_1samp(group1, 30)
print(f"One-Sample t-Test: t-statistic = {t_stat}, p-value = {p_value}")

# Independent Two-Sample t-Test (Testing if means of group1 and group2 are the same)
t_stat, p_value = stats.ttest_ind(group1, group2)
print(f"Two-Sample t-Test: t-statistic = {t_stat}, p-value = {p_value}")

# Interpret the results
alpha = 0.05
if p_value < alpha:
    print("Reject null hypothesis: There is a significant difference.")
else:
    print("Fail to reject null hypothesis: No significant difference.")
