# Linear Regression in Python

In this notebook, we will fit a simple linear regression model to data and visualize the regression line.

### Code:

```python
import numpy as np
import matplotlib.pyplot as plt
from sklearn.linear_model import LinearRegression

# Sample Data
np.random.seed(42)
X = np.random.normal(5, 2, 100).reshape(-1, 1)  # Independent variable
y = 3 * X + np.random.normal(0, 1, 100).reshape(-1, 1)  # Dependent variable with some noise

# Linear Regression Model
model = LinearRegression()
model.fit(X, y)

# Model coefficients
print(f"Intercept: {model.intercept_}")
print(f"Coefficient: {model.coef_}")

# Predictions
y_pred = model.predict(X)

# Plotting the regression line
plt.scatter(X, y, color='blue', label='Data')
plt.plot(X, y_pred, color='red', label='Regression Line')
plt.title('Linear Regression')
plt.xlabel('X')
plt.ylabel('y')
plt.legend()
plt.show()
