# Time Series Analysis in Python

This notebook demonstrates how to handle and visualize time series data, including decomposition and moving averages.

### Code:

```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import statsmodels.api as sm

# Generate Sample Time Series Data
np.random.seed(42)
time = pd.date_range(start='2020-01-01', periods=100, freq='D')
data = np.random.normal(0, 1, 100).cumsum()  # Cumulative sum to simulate a time series

# Create DataFrame
ts = pd.DataFrame(data, index=time, columns=['Value'])

# Plot the Time Series
ts.plot()
plt.title('Time Series Plot')
plt.xlabel('Date')
plt.ylabel('Value')
plt.show()

# Decompose the Time Series (Trend, Seasonality, Residuals)
decomposition = sm.tsa.seasonal_decompose(ts, model='additive')
decomposition.plot()
plt.show()

# Calculate Moving Average
ts['Moving_Avg'] = ts['Value'].rolling(window=7).mean()
ts[['Value', 'Moving_Avg']].plot()
plt.title('Time Series with Moving Average')
plt.show()
