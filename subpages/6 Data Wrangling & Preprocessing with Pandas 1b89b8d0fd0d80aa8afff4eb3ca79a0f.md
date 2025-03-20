# 6. Data Wrangling & Preprocessing with Pandas

Data Wrangling is a **crucial step** in data analysis that involves **cleaning, transforming,** and **organizing raw data** into a structured format for analysis. 

# Handling Missing Values

Missing values (`NaN` or `None`) are common in datasets. Pandas provides methods to **detect, fill,** or **drop** them.

## **Detect Missing Values**

```python
import pandas as pd
import numpy as np

data = {"Name":   ["Alice", "Bob", "Charlie", "David", np.nan],
				"Age":    [20, 30, np.nan, 40, 35],
				"Salary": [50000, np.nan, 70000, 80000, 60000]}
				
df = pd.DataFrame(data)
print(df.isnull())       # Check for missing values
print(df.isnull().sum()) # Count missing values per column
```

```
   Name    Age  Salary
0  False  False   False
1  False  False    True
2  False   True   False
3  False  False   False
4   True  False   False

Name      1
Age       1
Salary    1
dtype: int64
```

## **Dropping Missing Values**

```python
df_cleaned = pd.dropna() # Removes rows with NaN values
print(df_cleaned)
```

```
    Name   Age   Salary
0  Alice  20.0  50000.0
3  David  40.0  80000.0
```

## **Filling Missing Values**

```python
# re-run dataframe creation
df["Age"].fillna(df["Age"].mean(), inplace=True) # Fill with column mean
df["Salary"].fillna(0, inplace=True)             # Fill with 0
df["Name"].fillna("Unknown", inplace=True)       # Fill with a placeholder

print(df)
```

```
      Name    Age   Salary
0    Alice  20.00  50000.0
1      Bob  30.00      0.0
2  Charlie  31.25  70000.0
3    David  40.00  80000.0
4  Unknown  35.00  60000.0
```

# Removing Duplicates

Duplicate records can **skew analysis** and **inflate counts.**

## **Identifying Duplicates**

```python
df_dupes = pd.DataFrame({
													"ID": [1, 2, 2, 3, 4, 4],
													"Name": ["Alice", "Bob", "Bob", "Charlie", "David", "David"]
												})
												
print(df_dupes.duplicated()) # Identify duplicates
```

```
0    False
1    False
2     True
3    False
4    False
5     True
dtype: bool
```

## **Drop Duplicates**

```python
print(df_dupes)
print()

df_no_dupes = df_dupes.drop_duplicates()
print(df_no_dupes)
```

```
   ID     Name
0   1    Alice
1   2      Bob
2   2      Bob
3   3  Charlie
4   4    David
5   4    David

   ID     Name
0   1    Alice
1   2      Bob
3   3  Charlie
4   4    David
```

# Correcting Inconsistent Data

Data often has **formatting issues, typos,** or **mixed types.**

## **Standardizing Categorical Data**

```python
df_typos = pd.DataFrame({"City": ["New York", "new york", "NYC", "Los Angeles", "LA", "la"]})
print(df_typos)
print()

df_typos["City"] = df_typos["City"].str.lower().replace({"nyc": "new york", "la": "Los angeles"})
print(df_typos)
```

```
          City
0     New York
1     new york
2          NYC
3  Los Angeles
4           LA
5           la

          City
0     new york
1     new york
2     new york
3  los angeles
4  Los angeles
5  Los angeles
```

## **Converting Data Types**

```python
df["Age"] = df["Age"].astype(int) # Convert float to int
```

# Filtering & Sorting Data

## **Filtering Rows**

```python
data = {"Name":   ["Alice", "Bob", "Charlie", "David", np.nan],
				"Age":    [20, 30, np.nan, 40, 35],
				"Salary": [50000, np.nan, 70000, 80000, 60000]}
				
df = pd.DataFrame(data)

high_salary = df[df["Salary"] > 50000]
print(high_salary)
```

```
      Name   Age   Salary
2  Charlie   NaN  70000.0
3    David  40.0  80000.0
4      NaN  35.0  60000.0
```

## **Sorting Data**

```python
df_sorted = df.sort_values(by="Age", ascending=False)
print(df_sorted)
```

```
      Name   Age   Salary
3    David  40.0  80000.0
4      NaN  35.0  60000.0
1      Bob  30.0      NaN
0    Alice  20.0  50000.0
2  Charlie   NaN  70000.0
```

# Grouping & Aggregating Data

Grouping helps **summarize** datasets.

## **Grouping by Category**

```python
df_grouped = pd.DataFrame({"Department": ["HR", "HR", "IT", "IT", "Sales"],
													 "Salary": [50000, 52000, 70000, 75000, 60000]})
													 
grouped = df_grouped.groupby("Department").mean()
print(grouped)
```

```
             Salary
Department         
HR          51000.0
IT          72500.0
Sales       60000.0
```

# Data Transformation Pipelines

A **pipeline** applies multiple transformations **step-by-step.**

```python
def clean_data(df):
		df.drop_duplicates(inplace=True)
		df.fillna(df.mean(numeric_only=True), inplace=True)
		df["Age"] = df["Age"].astype(int)
		return df
		
df_cleaned = clean_data(df) 
# Duplicates removed, missing values filled, types corrected
```

# Practice Problems

## **Handling Missing Values**

Create a DataFrame with missing values and:

- Drop rows with NaNs.
- Fill missing numeric columns with their mean.

```python
data_missing = {"Name": ["Alice", "Bob", np.nan, "David", "Eve"],
								"Age": [25, np.nan, 30, 40, np.nan],
								"Salary": [50000, 60000, np.nan, 80000, 55000]}
								
df_missing = pd.DataFrame(data_missing)

# Dropping rows with missing values
df_dropped = df_missing.dropna()

# Filling missing numberic values with column mean
df_filled = df_missing.copy()
df_filled["Age"].fillna(df_missing["Age"].mean(), inplace=True)
df_filled["Salary"].fillna(df_missing["Salary"].mean(), inplace=True)

print("Before:")
print(df_missing)
print()
print("After:")
print(df_filled)
```

```
Before:
    Name   Age   Salary
0  Alice  25.0  50000.0
1    Bob   NaN  60000.0
2    NaN  30.0      NaN
3  David  40.0  80000.0
4    Eve   NaN  55000.0

After:
    Name        Age   Salary
0  Alice  25.000000  50000.0
1    Bob  31.666667  60000.0
2    NaN  30.000000  61250.0
3  David  40.000000  80000.0
4    Eve  31.666667  55000.0
```

## **Removing Duplicates**

Creating a DataFrame with duplicate rows and remove them.

```python
data_dupes = {"ID": [1, 2, 2, 3, 4, 4, 5],
							"Name": ["Alice", "Bob", "Bob", "Charlie", "David", "David", "Eve"]}
							
df_dupes = pd.DataFrame(data_dupes)
print("Before:")
print(df_dupes)
print()
df_no_dupes = df_dupes.drop_duplicates()
print("After:")
print(df_no_dupes)
```

```
Before:
   ID     Name
0   1    Alice
1   2      Bob
2   2      Bob
3   3  Charlie
4   4    David
5   4    David
6   5      Eve

After:
   ID     Name
0   1    Alice
1   2      Bob
3   3  Charlie
4   4    David
6   5      Eve
```

## **Filtering & Sorting:**

- Filter records where Salary > $50,000.
- Sort records by Age descending.

```python
df_salary = pd.DataFrame({"Name": ["Alice", "Bob", "Charlie", "David", "Eve"],
													 "Age": [25, 30, 35, 40, 29],
													 "Salary": [50000, 45000, 70000, 80000, 60000]})
													 
# Filtering salary > 50000
df_filtered = df_salary[df_salary["Salary"] > 50000]
print("Salary above $50,000:")
print(df_filtered)
print()

# Sorting by Age descending
print("Age Descending:")
df_sorted = df_salary.sort_values(by="Age", ascending=False)
print(df_sorted)
```

```
Salary above $50,000:
      Name  Age  Salary
2  Charlie   35   70000
3    David   40   80000
4      Eve   29   60000

Age Descending:
      Name  Age  Salary
3    David   40   80000
2  Charlie   35   70000
1      Bob   30   45000
4      Eve   29   60000
0    Alice   25   50000
```

## **Grouping & Aggregating**

Group employees by **department** and calculate the **average salary per department.**

```python
df_departments = pd.DataFrame({"Employee": ["Alice", "Bob", "Charlie", "David", "Eve"],
															 "Department": ["HR", "HR", "IT", "IT", "Sales"],
															 "Salary": [50000, 52000, 70000, 75000, 60000]})

print("Before:")
print(df_departments)
print()															 

# Grouping by department and calculating average salary
df_grouped = df_departments.groupby("Department").mean(numeric_only=True)
print("After:")
print(df_grouped)  													
```

```
Before:
  Employee Department  Salary
0    Alice         HR   50000
1      Bob         HR   52000
2  Charlie         IT   70000
3    David         IT   75000
4      Eve      Sales   60000

After:
             Salary
Department         
HR          51000.0
IT          72500.0
Sales       60000.0
```