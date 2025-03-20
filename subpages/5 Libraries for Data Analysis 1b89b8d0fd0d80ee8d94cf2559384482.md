# 5. Libraries for Data Analysis

# NumPy - Numerical Computation & Arrays

NumPy (**Numerical Python**) is used for fast array operations, mathematical calculations, and matrix operations. 

## **Installing NumPy**

```python
pip install numpy
```

View NumPy documentation for more info: https://numpy.org/doc/

## 1D Arrays

A **one-dimensional (1D) array** is similar to a list but more efficient.

```python
import numpy as np

arr1D = np.array([10, 20, 30, 40, 50])
print(arr1D)
print("Shape:", arr1D.shape)
print("Data Type:", arr1D.dtype)
```

```
[10 20 30 40 50]
Shape: (5,)
Data Type: int32
```

### **Array Operations**

```python
arr = np.array([1, 2, 3, 4, 5])

print("Sum:", np.sum(arr))
print("Mean:", np.mean(arr))
print("Standard Deviation:", np.std(arr))
print("Max:", np.max(arr))
print("Min:", np.min(arr))
print("Squared:", arr ** 2)

```

```
Sum: 15
Mean: 3.0
Standard Deviation: 1.4142135623730951
Max: 5
Min: 1
Squared: [ 1  4  9 16 25]
```

## 2D Arrays (Matrices)

A **two-dimensional (2D) array** is a matrix.

```python
matrix = np.array([[1, 2, 3], [4, 5, 6]])

print(matrix)
print("Shape:", matrix.shape)
```

```
[[1 2 3]
 [4 5 6]]
Shape: (2, 3)
```

### **Matrix Operations**

```python
print("Transpose:\n", matrix.T)
print("Element-wise multiplication:\n", matrix * 2)
print("Dot Product:\n", np.dot(matrix, matrix.T))
```

```
Transpose:
 [[1 4]
 [2 5]
 [3 6]]
Element-wise multiplication:
 [[ 2  4  6]
 [ 8 10 12]]
Dot Product:
 [[14 32]
 [32 77]]
```

## Slicing & Indexing

```python
arr = np.array([[10, 20, 30], [40, 50, 60]])

print(arr[0, 1])  # Access row 0, column 1 (20)
print(arr[:, 1])  # All rows, column 1
print(arr[0, :])  # Row 0, all columns
```

```
20
[20 50]
[10 20 30]
```

# Pandas - Data Manipulation

Pandas is used for working with **structured data** (CSV, Excel, SQL tables, JSON).

## **Installing Pandas**

```
pip install pandas
```

View Pandas documentation for more info: https://pandas.pydata.org/docs/

## Creating a DataFrame

```python
import pandas as pd

data = {
					"Product": ["Laptop", "Mouse", "Keyboard"],
					"Price":   [1000, 25, 45],
					"Stock":   [10, 50, 30]
			 }
df = pd.DataFrame(data)
print(df)
```

```
    Product  Price  Stock
0    Laptop   1000     10
1     Mouse     25     50
2  Keyboard     45     30
```

## Reading & Writing Files

```python
df.to_csv("products.csv", index=False) # Save to CSV
df2 = pd.read_csv("products.csv")      # Read CSV
```

## Filtering & Querying Data

```python
filtered_df = df[df["Price"] > 50]
print(filtered_df)
```

```
Product  Price  Stock
0  Laptop   1000     10
```

## Handling Missing Data

```python
print(df)
df["Stock"] = df["Stock"].replace(30, np.nan)
df.fillna(0, inplace=True) # Replace NaN with 0
print(df)
```

```
Product  Price  Stock
0    Laptop   1000     10
1     Mouse     25     50
2  Keyboard     45     30
    Product  Price  Stock
0    Laptop   1000   10.0
1     Mouse     25   50.0
2  Keyboard     45    0.0
```

# Matplotlib - Data Visualization

Matplotlib is used to create **static** visualizations.

## **Installing Matplotlib**

```
pip install matplotlib
```

View Matplotlib documentation for more info: https://matplotlib.org/stable/index.html

## Creating a Line Plot

```python
import matplotlib.pyplot as plt

x = [1, 2, 3, 4, 5]
y = [10, 20, 15, 25, 30]

plt.plot(x, y, marker="o", linestyle="--", color="red")
plt.xlabel("X-axis")
plt.ylabel("Y-axis")
plt.title("Sample Line Plot")
plt.show()
```

![image.png](5%20Libraries%20for%20Data%20Analysis%201b89b8d0fd0d80ee8d94cf2559384482/image.png)

## Creating a Bar Chart

```python
categories = ["A", "B", "C"]
values = [5, 7, 3]

plt.bar(categories, values, color="blue")
plt.xlabel("Categories")
plt.ylabel("Values")
plt.title("Bar Chart Example")
plt.show()
```

![image.png](5%20Libraries%20for%20Data%20Analysis%201b89b8d0fd0d80ee8d94cf2559384482/image%201.png)

# Seaborn

Seaborn provides **beautiful** and **statistical** plots.

## **Installing Seaborn**

```
pip install seaborn
```

View Seaborn documentation for more info: https://seaborn.pydata.org/

## Creating a Histogram

```python
import seaborn as sns

data = [50, 52, 60, 63, 65, 66, 67, 70, 75, 80, 85]
sns.histplot(data, bins=5, kde=True)
plt.title("Age Distribution")
plt.show()
```

![image.png](5%20Libraries%20for%20Data%20Analysis%201b89b8d0fd0d80ee8d94cf2559384482/image%202.png)

## Creating a Heatmap

```python
matrix = np.random.rand(5, 5)

sns.heatmap(matrix, annot=True, cmap="coolwarm")
plt.title("Heatmap Example")
plt.show()
```

![image.png](5%20Libraries%20for%20Data%20Analysis%201b89b8d0fd0d80ee8d94cf2559384482/image%203.png)

# SciPy - Scientific Computing

SciPy is used for **statistical functions, optimization, and probability distributions.**

## **Installing SciPy**

```
pip install scipy
```

View SciPy documentation for more info: https://docs.scipy.org/doc/scipy/

## Calculating Statistical Measures

```python
from scipy import stats

data = [10, 20, 30, 40, 50, 60, 70]

print("Mean:", stats.mean(data))
print("Median:", stats.median(data))
print("Mode:", stats.mode(data))
```

```
Mean: 38.75
Median: 35.0
Mode: ModeResult(mode=np.int64(30), count=np.int64(2))
```

# Plotly - Interactive Visualizations

Plotly is used for **interactive charts.**

## **Installing Plotly**

```
pip install plotly
```

View Plotly documentation for more info: https://plotly.com/python/

## Creating an Interactive Line Chart

```python
import plotly.express as px

df = pd.DataFrame({"X": [1, 2, 3, 4, 5], "Y": [10, 20, 15, 25, 30]})
fig = px.line(df, x="X", y="Y", title="Interactive Line Chart")
fig.show()
```

![newplot.png](5%20Libraries%20for%20Data%20Analysis%201b89b8d0fd0d80ee8d94cf2559384482/newplot.png)

# Practice Problems

## **NumPy**

Create a **2D matrix**, get **sum, mean,** and **standard deviation.**

```python
import numpy as np

matrix = np.array([[10, 20, 30], [40, 50, 60], [70, 80, 90]])

print("Sum:", np.sum(matrix))
print("Mean:", np.mean(matrix))
print("Standard Deviation:", np.std(matrix))
```

```
Sum: 450
Mean: 50.0
Standard Deviation: 25.81988897471611
```

## **Pandas**

Load a CSV, **filter rows** where price > 50.

```python
import pandas as pd

data = {
					"Product": ["Laptop", "Mouse", "Keyboard", "Monitor"],
					"Price":   [1000, 25, 45, 150],
					"Stock":   [10, 50, 30, 20]
			 }
			 
df = pd.DataFrame(data)
df.to_csv("data.csv", index=False)

df1 = pd.read_csv("data.csv")
filtered_df = df[df["Price"] > 50]
```

```
   Product  Price  Stock
0   Laptop   1000     10
3  Monitor    150     20
```

## **Matplotlib**

Create a **bar chart** for sales data.

```python
import matplotlib.pyplot as plt

categories = ["January", "February", "March"]
sales = [100, 15, 200]

plt.bar(categories, sales, color="skyblue")
plt.xlabel("Months")
plt.ylabel("Sales")
plt.title("Monthly Sales Data")
plt.show()
```

![image.png](5%20Libraries%20for%20Data%20Analysis%201b89b8d0fd0d80ee8d94cf2559384482/image%204.png)

## **Seaborn**

Generate **100 random numbers**, create a histogram.

```python
import seaborn as sns

random_data = np.random.normal(loc=50, scale=15, size=100)

sns.histplot(random_data, bins=10, kde=True)
plt.title("Random Data Distribution")
plt.show()
```

![image.png](5%20Libraries%20for%20Data%20Analysis%201b89b8d0fd0d80ee8d94cf2559384482/image%205.png)

## **SciPy**

Generate **20 random numbers**, compute **mean, median,** and **mode.**

```python
from scipy import stats

random_numbers = np.random.randint(1, 100, 20)

print("Mean:", stats.tmean(random_numbers))
print("Median:", np.median(random_numbers))  # Use numpy's median
print("Mode:", stats.mode(random_numbers, keepdims=True).mode[0])  # Use stats.mode() correctly
```

```
Mean: 48.0
Median: 52.5
Mode: 13
```

## **Plotly**

Create an **interactive scatter plot.**

```python
import plotly.express as px

df_plotly = pd.DataFrame({"X": [1, 2, 3, 4, 5], "Y": [100, 150, 200, 250, 300]})
fig = px.scatter(df_plotly, x="X", y="Y", title="Interactive Scatter Plot")
fig.show()
```

![newplot.png](5%20Libraries%20for%20Data%20Analysis%201b89b8d0fd0d80ee8d94cf2559384482/newplot%201.png)