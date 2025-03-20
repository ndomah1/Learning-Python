# 9. Exploratory Data Analysis (EDA) Guide

Exploratory Data Analysis (**EDA**) is the **first step** in understanding a dataset. Before performing formal analysis or modeling, EDA helps uncover **patterns, trends,** and **outliers.**

# Descriptive Statistics

- Summarizing Data

Pandas provides `.describe()` to computer common statistics.

```python
import pandas as pd
import numpy as np

# Sample dataset
data = {"Age": [22, 25, 47, 35, 46, 50, 23, 25, 40, 39],
				"Salary": [30000, 32000, 70000, 45000, 68000, 75000, 32000, 33000, 55000, 52000]}
df = pd.DataFrame(data)

# Summary statistics
print(df.describe())				
```

```
             Age        Salary
count  10.000000     10.000000
mean   35.200000  49200.000000
std    10.768266  17427.946905
min    22.000000  30000.000000
25%    25.000000  32250.000000
50%    37.000000  48500.000000
75%    44.500000  64750.000000
max    50.000000  75000.000000
```

- **Mean (Average)**: `df.mean()`
- **Median:** `df.median()`
- **Standard Deviation**: `df.std()`
- **Skewness (symmetry of data)**: `df.skew()`
- **Kurtosis (tailedness of data):** `df.kurt()`

# Understanding Data Distributions

## **Histograms - Checking the Spread of Data**

A histogram helps visualize how data is distributed

```python
import matplotlib.pyplot as plt
import seaborn as sns

sns.histplot(df["Age"], bins=5, kde=True)
plt.title("Age Distributions")
plt.show()
```

![image.png](9%20Exploratory%20Data%20Analysis%20(EDA)%20Guide%201b89b8d0fd0d80cf9d05d92500c5f9e5/image.png)

## Box Plots - Detecting Outliers

A box plot shows **median, quartiles,** and **outliers.**

```python
sns.boxplot(x=df["Salary"])
plt.title("Salary Box Plot")
plt.show()
```

![image.png](9%20Exploratory%20Data%20Analysis%20(EDA)%20Guide%201b89b8d0fd0d80cf9d05d92500c5f9e5/image%201.png)

# Identifying Relationships Between Variables

## Scatter Plot - Checking Correlations

A scatter plot helps visualize **relationships** between variables.

```python
sns.scatterplot(x=df["Age"], y=df["Salary"])
plt.title("Age vs. Salary")
plt.show()
```

![image.png](9%20Exploratory%20Data%20Analysis%20(EDA)%20Guide%201b89b8d0fd0d80cf9d05d92500c5f9e5/image%202.png)

## Correlation Matrix - How Strong are Relationships?

```python
print(df.corr())  # Computer correlation coefficients

sns.heatmap(df.corr(), annot=True, cmap="coolwarm")
plt.title("Correlation Matrix")
plt.show()
```

![image.png](9%20Exploratory%20Data%20Analysis%20(EDA)%20Guide%201b89b8d0fd0d80cf9d05d92500c5f9e5/image%203.png)

# Detecting Outliers

Outliers can **skew analysis** and need to be handled carefully.

## Z-Score Method

A Z-score tells how many **standard deviations** a value is from the mean.

```python
data = {
 "Age": [22, 25, 47, 35, 46, 50, 23, 25, 40, 39],
 "Salary": [30000, 32000, 1000000, 45000, 68000, 75000, 32000, 33000, 99000, 52000]
}

df = pd.DataFrame(data)

from scipy.stats import zscore

df["Z_Score"] = zscore(df["Salary"])
outliers = df[df["Z_Score"].abs() > 2]
print(outliers)
```

```
   Age   Salary   Z_Score
2   47  1000000  2.991348
```

Rows with **`Salary` values outside 2 standard deviations.**

## Interquartile Range (IQR) Method

```python
Q1 = df["Salary"].quantile(0.25)
Q3 = df["Salary"].quantile(0.75)
IQR = Q3 - Q1

outliers_iqr = df[(df["Salary"] < (Q1 - 1.5 * IQR)) | (df["Salary"] > (Q3 + 1.5 * IQR))]
print(outliers_iqr)
```

```
   Age   Salary   Z_Score
2   47  1000000  2.991348
```

Rows outside the **normal range of `Salary` .**

# Practice Problems

## Summarizing Data

Use `.describe()` on a dataset and extract the **mean, median, standard deviation.**

```python
print(df.describe())
```

```
             Age          Salary    Z_Score
count  10.000000       10.000000  10.000000
mean   35.200000   146600.000000   0.000000
std    10.768266   300721.428864   1.054093
min    22.000000    30000.000000  -0.408708
25%    25.000000    32250.000000  -0.400821
50%    37.000000    48500.000000  -0.343861
75%    44.500000    73250.000000  -0.257107
max    50.000000  1000000.000000   2.991348
```

## Data Distribution

Plot a **histogram** and **box plot** for Salary.

```python
plt.figure(figsize=(12, 5))

# Histogram
plt.subplot(1, 2, 1)
sns.histplot(df["Salary"], bins=5, kde=True, color="skyblue")
plt.title("Salary Distribution")

# Box Plot
plt.subplot(1, 2, 2)
sns.boxplot(x=df["Salary"], color="lightcoral")
plt.title("Salary Box Plot")

plt.show()
```

![image.png](9%20Exploratory%20Data%20Analysis%20(EDA)%20Guide%201b89b8d0fd0d80cf9d05d92500c5f9e5/image%204.png)

## Relationships

Create a **scatter plot** of Age vs Salary and compute the **correlation matrix.**

```python
plt.figure(figsize=(12, 5))

# Scatter Plot
plt.subplot(1, 2, 1)
sns.scatterplot(x=df["Age"], y=df["Salary"], color="green")
plt.title("Age vs Salary")

# Correlation Matrix
plt.subplot(1, 2, 2)
sns.heatmap(df.corr(), annot=True, cmap="coolwarm", linewidths=0.5)
plt.title("Correlation Matrix")

plt.show()
```

![image.png](9%20Exploratory%20Data%20Analysis%20(EDA)%20Guide%201b89b8d0fd0d80cf9d05d92500c5f9e5/image%205.png)

## Outlier Detection

Identify outliers using **Z-score** and **IQR methods.**

```python
from scipy.stats import zscore

df["Z_Score"] = zscore(df["Salary"])
outliers_z = df[df["Z_Score"].abs() > 2]

Q1 = df["Salary"].quantile(0.25)
Q3 = df["Salary"].quantile(0.75)
IQR = Q3 - Q1

outliers_iqr = df[(df["Salary"] < (Q1 - 1.5 * IQR)) | (df["Salary"] > (Q3 + 1.5 * IQR))]
print(outliers_iqr)
```

```
   Age   Salary   Z_Score
2   47  1000000  2.991348
```