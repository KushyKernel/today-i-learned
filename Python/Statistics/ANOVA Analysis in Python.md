# ANOVA Analysis in Python

This notebook demonstrates how to perform one-way ANOVA to test if the means of multiple groups are statistically different.

### Code:

```python
import numpy as np
import scipy.stats as stats

# Sample Data (3 groups)
group1 = [22, 24, 27, 29, 31]
group2 = [18, 21, 25, 27, 30]
group3 = [30, 32, 34, 36, 40]

# Perform One-Way ANOVA
f_stat, p_value = stats.f_oneway(group1, group2, group3)
print(f"ANOVA Test: F-statistic = {f_stat}, p-value = {p_value}")

# Interpret the results
alpha = 0.05
if p_value < alpha:
    print("Reject null hypothesis: There is a significant difference between the groups.")
else:
    print("Fail to reject null hypothesis: No significant difference between the groups.")
