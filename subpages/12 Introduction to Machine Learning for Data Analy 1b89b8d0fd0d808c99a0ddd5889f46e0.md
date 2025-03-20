# 12. Introduction to Machine Learning for Data Analysts

Machine Learning (**ML**) is a powerful tool for making **predictions** and finding **patterns** in data.

# Supervised vs. Unsupervised Learning

Machine learning models learn patterns from **historical data.**

## Supervised Learning - When the data has labels (X → Y)

- Used for predictions.
- Examples:
    - **Regression:** Predicting sales based on marketing spend.
    - **Classification:** Detecting spam emails.

## Unsupervised Learning - When data has no labels

- Used for finding hidden patterns.
- Examples:
    - **Clustering:** Grouping customers by purchasing behavior.
    - **Dimensionality Reduction:** Compressing large datasets while keeping information.

# Basic ML Workflow

Machine learning follows these key steps:

1. **Load Data** → Use CSVs, databases, or APIs.
2. **Split Data** → Separate into **training** (80%) and **testing** (20%) sets.
3. **Train a Model** → Fit an ML model on training data. 
4. **Evaluate Performance** → Check accuracy on test data.

# Simple ML Algorithms

## Linear Regression (Supervised Learning)

Used for **predicting numerical values.**

Example: **Predicting house prices** based on square footage.

```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
from sklearn.model_selection import train_test_split
from sklearn.linear_model import LinearRegression
from sklearn.metrics import mean_absolute_error, mean_squared_error

# Generate sample data
np.random.seed(42)
square_feet = np.random.randint(500, 3000, 50)  # House sizes
prices = square_feet * 100 + np.random.randint(-5000, 5000, 50)  # House prices with noise

# Convert to DataFrame
df = pd.DataFrame({"Square_Feet": square_feet, "Price": prices})

# Split into training and testing sets
X = df[["Square_Feet"]]
y = df["Price"]
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)

# Train Linear Regression Model
model = LinearRegression()
model.fit(X_train, y_train)

# Predict on test data
y_pred = model.predict(X_test)

# Evaluate model performance
mae = mean_absolute_error(y_test, y_pred)
mse = mean_squared_error(y_test, y_pred)

print("✅ Model Trained Successfully")
print("Mean Absolute Error (MAE):", mae)
print("Mean Squared Error (MSE):", mse)

# Plot results
plt.scatter(X_test, y_test, color="blue", label="Actual Prices")
plt.plot(X_test, y_pred, color="red", linewidth=2, label="Predicted Prices")
plt.xlabel("Square Feet")
plt.ylabel("House Price")
plt.title("Linear Regression: House Prices Prediction")
plt.legend()
plt.show()
```

```
✅ Model Trained Successfully
Mean Absolute Error (MAE): 1898.1729913857853
Mean Squared Error (MSE): 5014004.615503585
```

![image.png](12%20Introduction%20to%20Machine%20Learning%20for%20Data%20Analy%201b89b8d0fd0d808c99a0ddd5889f46e0/image.png)

## K-Means Clustering (Unsupervised Learning)

Used for **grouping similar data points.**

Example: **Segmenting customers based on purchase history.**

```python
from sklearn.cluster import KMeans
import seaborn as sns

# Generate random customer data
np.random.seed(42)
customers = pd.DataFrame({
 "Annual_Income": np.random.randint(20000, 100000, 50),
 "Spending_Score": np.random.randint(1, 100, 50)
})

# Train K-Means with 3 clusters
kmeans = KMeans(n_clusters=3, random_state=42)
customers["Cluster"] = kmeans.fit_predict(customers)

# Visualize Clusters
sns.scatterplot(x=customers["Annual_Income"], y=customers["Spending_Score"], hue=customers["Cluster"])
plt.title("Customer Segmentation using K-Means Clustering")
plt.xlabel("Annual Income ($)")
plt.ylabel("Spending Score")
plt.show()
```

![image.png](12%20Introduction%20to%20Machine%20Learning%20for%20Data%20Analy%201b89b8d0fd0d808c99a0ddd5889f46e0/image%201.png)

# Practice Problems

## Linear Regression

Train a linear regression model to predict house prices based on square footage.

```python
# Generate sample data for house prices
np.random.seed(42)
square_feet = np.random.randint(500, 3000, 50) # House sizes
prices = square_feet * 100 + np.random.randint(-5000, 5000, 50) # House prices with noise

# Convert to DataFrame
df_houses = pd.DataFrame({"Square_Feet": square_feet, "Price": prices})

# Split into training and testing sets
X = df_houses[["Square_Feet"]]
y = df_houses["Price"]
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)

# Train Linear Regression model
model = LinearRegression()
model.fit(X_train, y_train)

# Predict on test data
y_pred = model.predict(X_test)

# Evaluate model performance
mae = mean_absolute_error(y_test, y_pred)
mse = mean_squared_error(y_test, y_pred)

# Display Linear Regression Results
plt.scatter(X_test, y_test, color="blue", label="Actual Prices")
plt.plot(X_test, y_pred, color="red", linewidth=2, label="Predicted Prices")
plt.xlabel("Square Feet")
plt.ylabel("House Price")
plt.title("Linear Regression: House Prices Prediction")
plt.legend()
```

![image.png](12%20Introduction%20to%20Machine%20Learning%20for%20Data%20Analy%201b89b8d0fd0d808c99a0ddd5889f46e0/image%202.png)

## K-Means Clustering

Use K-Means clustering to group customers based on **income** and **spending habits.**

```python
np.random.seed(42)
customers = pd.DataFrame({
 "Annual_Income": np.random.randint(20000, 100000, 50),
 "Spending_Score": np.random.randint(1, 100, 50)
})
# Train K-Means with 3 clusters
kmeans = KMeans(n_clusters=3, random_state=42, n_init=10)
customers["Cluster"] = kmeans.fit_predict(customers)
# Visualize Clusters
sns.scatterplot(x=customers["Annual_Income"], y=customers["Spending_Score"], hue=customers["Cluster
plt.title("Customer Segmentation using K-Means Clustering")
plt.xlabel("Annual Income ($)")
plt.ylabel("Spending Score")
plt.show()
```

![image.png](12%20Introduction%20to%20Machine%20Learning%20for%20Data%20Analy%201b89b8d0fd0d808c99a0ddd5889f46e0/image%203.png)

## Model Evaluation

Compute **Mean Absolute Error (MAE)** and **Mean Squared Error (MSE)** for the regression model.

```python
# Evaluate model performance
mae = mean_absolute_error(y_test, y_pred)
mse = mean_squared_error(y_test, y_pred)
```