# 7. Data Visualization Principles

Data visualization is crucial for **communicating data insights effectively.** A well-designed chart **tells a story,** whereas a poor visualization can be **misleading** or **confusing.**

# Choosing the Right Chart Type

| Chart Type | Best For |
| --- | --- |
| Line Chart | Trends over time (e.g., sales over months) |
| Bar Chart | Comparing categories (e.g., revenue by region) |
| Pie Chart | Showing parts of a whole (e.g., market share) |
| Scatter Plot | Showing relationships between variables (e.g., age vs income) |
| Histogram | Visualizing distributions (e.g., exam scores) |
| Box Plot | Identifying outliers and quartiles (e.g., salaries in a company) |

# Best Practices for Effective Visualizations

To **communicate insights clearly,** follow these best practices:

- **Always Label Axes & Titles** - Readers should instantly understand the chart.
- **Use the Right Scale** - Avoid distorting data with improper axis scaling.
- **Choose the Right Colors** - Use distinct colors but avoid excessive variety.
- **Highlight Key Insights** - Use annotations, text, or color emphasis.
- **Avoid Clutter** - Simplify by removing unnecessary elements.

# Effective Design Principles

## Keep it Simple

A clean chart is easier to **read** and **interpret.**

```python
import matplotlib.pyplot as plt

x = ["A", "B", "C", "D"]
y = [10, 25, 15, 30]

plt.bar(x, y, color="skyblue")
plt.xlabel("Categories")
plt.ylabel("Values")
plt.title("Simple Bar Chart")
plt.show()
```

![image.png](7%20Data%20Visualization%20Principles%201b89b8d0fd0d80599bd7d3596e2ded50/image.png)

- Common bad examples:
    - Too many colors
    - No labels
    - Unnecessary 3D effects

## Use the Right Scale

A **misleading y-axis** can distort data.

**BAD EXAMPLE**

```python
plt.bar(x, y, color="red")
plt.ylim(10, 30) # Cropping data to make differences appear larger
plt.show()
```

![image.png](7%20Data%20Visualization%20Principles%201b89b8d0fd0d80599bd7d3596e2ded50/image%201.png)

**GOOD EXAMPLE**

```python
plt.bar(x, y, color="green")
plt.ylim(0, 35) # Showing full range for honest comparison
plt.show()
```

![image.png](7%20Data%20Visualization%20Principles%201b89b8d0fd0d80599bd7d3596e2ded50/image%202.png)

## Highlight Key Insights

Make **important trends stand out.**

**GOOD EXAMPLE**

```python
plt.plot(["Jan", "Feb", "Mar", "Apr"], [100, 200, 250, 180], marker="o", label="Sales")
plt.axhline(200, color="red", linestyle="--", label="Target")
plt.title("Sales Growth with Target Line")
plt.legend()
plt.show()
```

![image.png](7%20Data%20Visualization%20Principles%201b89b8d0fd0d80599bd7d3596e2ded50/image%203.png)

- Highlights where sales **exceed** or **miss targets.**

## Common Pitfalls to Avoid

- Pie charts with too many slices.
    - Bad when there are too many categories! Use a **bar chart** instead.
- Overcomplicated legends and labels.
    - Avoid excessive text, labels, and gridlines.
    - Use concise labels and a simple color scheme instead.
- Using 3D graphs unnecessarily.
    - 3D charts are hard to interpret correctly.
    - Stick to 2D charts unless 3D is essential.

# Practical Examples

## **Example 1: Line Chart (Trends)**

```python
months = ["Jan", "Feb", "Mar", "Apr"]
sales = [100, 150, 200, 250]

plt.plot(months, sales, marker="o", linestyle="--", color="blue")
plt.xlabel("Month")
plt.ylabel("Sales ($)")
plt.title("Sales Trend Over Time")
plt.show()
```

![image.png](7%20Data%20Visualization%20Principles%201b89b8d0fd0d80599bd7d3596e2ded50/image%204.png)

## **Example 2: Scatter Plot (Relationships)**

```python
import numpy as np
import seaborn as sns

x = np.random.rand(50) * 100
y = x + (np.random.rand(50) * 10)  # Adding slight variation

sns.scatterplot(x=x, y=y)
plt.xlabel("Variable X")
plt.ylabel("Variable Y")
plt.title("Scatter Plot Showing Relationship")
plt.show()
```

![image.png](7%20Data%20Visualization%20Principles%201b89b8d0fd0d80599bd7d3596e2ded50/image%205.png)

## **Example 3: Histogram (Distributions)**

```python
data = np.random.normal(loc=50, scale=15, size=1000)

sns.histplot(data, bins=30, kde=True)
plt.xlabel("Value")
plt.ylabel("Frequency")
plt.title("Histogram of Data Distribution")
plt.show()
```

![image.png](7%20Data%20Visualization%20Principles%201b89b8d0fd0d80599bd7d3596e2ded50/image%206.png)

## **Example 4: Box Plot (Outliers)**

```python
data = [25, 30, 45, 50, 55, 100]  # 100 is an outlier

sns.boxplot(data=data)
plt.title("Box Plot Showing Outlier")
plt.show()
```

![image.png](7%20Data%20Visualization%20Principles%201b89b8d0fd0d80599bd7d3596e2ded50/image%207.png)

# Practice Problems

## **Choosing the Right Chart Type**

- What type of chart would you use for:
    - Monthly website traffic? → Line chart (to show trends over time)
    - Comparing sales across regions? → Bar chart (for category comparisons)
    - Checking correlation between age and income? → Scatter plot (to identify relationships)

## **Visualize a Dataset:**

- Create a **line chart** for sales over 6 months.
    
    ```python
    months = ["Jan", "Feb", "Mar", "Apr", "May", "Jun"]
    sales = [500, 700, 900, 850, 1100, 1200]
    
    plt.figure(figsize=(10, 5))
    plt.plot(months, sales, marker="o", linestyle="--", color="blue")
    plt.xlabel("Months")
    plt.ylabel("Sales ($)")
    plt.title("Sales Trend Over 6 Months")
    plt.grid(True)
    plt.show()
    ```
    
    ![image.png](7%20Data%20Visualization%20Principles%201b89b8d0fd0d80599bd7d3596e2ded50/image%208.png)
    

## Create a **scatter plot** for two related variables.

```python
np.random.seed(42)
x_values = np.random.rand(50) * 100
y_values = x_values + (np.random.rand(50) * 20)  # Adding slight noise

plt.figure(figsize=(8, 5))
sns.scatterplot(x=x_values, y=y_values, color="red")
plt.xlabel("Variable X")
plt.ylabel("Variable Y")
plt.title("Scatter Plot of Two Related Variables")
plt.show()
```

![image.png](7%20Data%20Visualization%20Principles%201b89b8d0fd0d80599bd7d3596e2ded50/image%209.png)

## **Fix a Misleading Chart:**

- Create a **bar chart with a bad  y-axis scale** and correct it.
    
    ```python
    # Bad example
    plt.figure(figsize=(10, 5))
    plt.bar(months, sales, color="red")
    plt.ylim(600, 1300) # Cropping Y-axis
    plt.title("Misleading Bar Chart with Cropped Y-Axis")
    plt.show()
    ```
    
    ![image.png](7%20Data%20Visualization%20Principles%201b89b8d0fd0d80599bd7d3596e2ded50/image%2010.png)
    
    ```python
    # Corrected
    plt.figure(figsize=(10, 5))
    plt.bar(months, sales, color="green")
    plt.ylim(0, 1300)  # Full Y-axis scale for honest comparison
    plt.title("Corrected Bar Chart with Full Y-Axis")
    plt.show()
    ```
    
    ![image.png](7%20Data%20Visualization%20Principles%201b89b8d0fd0d80599bd7d3596e2ded50/image%2011.png)
    

## **Create a Box Plot:**

- Generate a data set and create a boxplot to **detect outliers.**

```python
data_with_outliers = [20, 25, 30, 40, 100]  # 100 is an outlier

plt.figure(figsize=(8,5))
sns.boxplot(data=data_with_outliers)
plt.title("Box Plot Showing Outliers")
plt.show()
```

![image.png](7%20Data%20Visualization%20Principles%201b89b8d0fd0d80599bd7d3596e2ded50/image%2012.png)