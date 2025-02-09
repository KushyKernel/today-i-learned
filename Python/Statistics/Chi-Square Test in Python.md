# Chi-Square Test in Python

This notebook demonstrates how to perform a chi-square test to determine if there is a significant difference between observed and expected frequencies.

### Code:

```python
import numpy as np
import scipy.stats as stats

# Observed frequencies for a categorical variable (example: gender distribution in a group)
observed = np.array([50, 30, 20])  # Observed frequencies for 3 categories

# Expected frequencies (uniform distribution assumption for example)
expected = np.array([33.33, 33.33, 33.33])

# Perform Chi-Square Test
chi2_stat, p_value = stats.chisquare(observed, expected)
print(f"Chi-Square Test: chi2_stat = {chi2_stat}, p-value = {p_value}")

# Interpretation
alpha = 0.05
if p_value < alpha:
    print("Reject null hypothesis: The observed distribution is significantly different from expected.")
else:
    print("Fail to reject null hypothesis: No significant difference between observed and expected.")
