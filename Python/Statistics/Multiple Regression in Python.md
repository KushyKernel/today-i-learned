# Multiple Regression in Python

This notebook demonstrates how to perform multiple regression with more than one predictor variable.

### Code:

```python
import numpy as np
import pandas as pd
import statsmodels.api as sm
from sklearn.model_selection import train_test_split
from sklearn.metrics import mean_squared_error

# Sample Data (multiple predictors)
np.random.seed(42)
X = np.random.normal(0, 1, (100, 3))  # 3 predictors
y = 3 * X[:, 0] - 2 * X[:, 1] + 1.5 * X[:, 2] + np.random.normal(0, 0.5, 100)  # Dependent variable

# Convert to DataFrame
df = pd.DataFrame(X, columns=['X1', 'X2', 'X3'])
df['y'] = y

# Splitting the data into training and test sets
X_train, X_test, y_train, y_test = train_test_split(df[['X1', 'X2', 'X3']], df['y'], test_size=0.2, random_state=42)

# Adding a constant for intercept in the model
X_train_const = sm.add_constant(X_train)

# Fitting the model using statsmodels
model = sm.OLS(y_train, X_train_const)
results = model.fit()

# Print the model summary
print(results.summary())

# Make predictions on the test set
X_test_const = sm.add_constant(X_test)
y_pred = results.predict(X_test_const)

# Calculate Mean Squared Error
mse = mean_squared_error(y_test, y_pred)
print(f"Mean Squared Error on Test Set: {mse}")
