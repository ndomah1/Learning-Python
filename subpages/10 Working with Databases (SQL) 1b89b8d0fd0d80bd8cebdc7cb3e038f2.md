# 10. Working with Databases (SQL)

As a **data analyst**, you must be proficient in **SQL** to retrieve, filter, and manipulate data from databases.

# SQL Basics

## Retrieving Data (`SELECT`)

The `SELECT` statement retrieves **specific columns** from a table.

```sql
SELECT first_name, last_name, age FROM employees;
```

| `first_name` | `last_name` | `age` |
| --- | --- | --- |
| Alice | Johnson | 30 |
| Bob | Smith | 25 |
| Charlie | Brown | 35 |

## Filtering Rows (`WHERE`)

The `WHERE` clause filters records **based on conditions.**

```sql
SELECT * FROM employees WHERE age > 30;
```

| `first_name` | `last_name` | `age` |
| --- | --- | --- |
| Charlie | Brown | 35 |

## Sorting Data (`ORDER BY`)

Sort data in **ascending** (`ASC`) or **descending** (`DESC`) order.

```sql
SELECT * FROM employees ORDER BY age DESC;
```

Sorts employees from **oldest** to **youngest.**

# Filtering & Aggregation

## Using Aggregate Functions

| Function | Description |
| --- | --- |
| `COUNT(*)` | Counts rows |
| `SUM(column)` | Adds values |
| `AVG(column)` | Calculates average |
| `MAX(column)` | Finds highest value |
| `MIN(column)` | Finds lowest value |

```sql
SELECT COUNT(*) FROM employees;
```

```
Total Employees: 50
```

## Grouping Data (`GROUP BY`)

Groups data into **categories** and applies aggregate functions.

```sql
SELECT department, AVG(salary) FROM employees GROUP BY department;
```

| `department` | `avg_salary` |
| --- | --- |
| HR | 60000 |
| IT | 75000 |
| Sales | 50000 |

## Filtering Aggregates (`HAVING`)

`HAVING` filters **after aggregation** (while `WHERE` filters before).

```sql
SELECT department, AVG(salary)
FROM employees
GROUP BY department
HAVING AVG(salary) > 60000;
```

Returns only departments with an average salary **above $60,000.**

# Joining Tables (`JOIN`)

Data is often stored across **multiple tables.** `JOIN` helps **combine related data.**

## Inner Join (`INNER JOIN`)

Returns only **matching records** from both tables.

```sql
SELECT e.first_name, e.last_name, d.deparment_name
FROM employees e
INNER JOIN departments d
		ON e.department_id = d.department_id;
```

| `first_name` | `last_name` | `department_name` |
| --- | --- | --- |
| Alice | Johnson | IT |
| Bob | Smith | HR |
| Charlie | Brown | Sales |

## Left Join (`LEFT JOIN`)

Returns **all records** from the **left table** and matching ones from the right.

```sql
SELECT e.first_name, e.last_name, d.department_name
FROM employees e
LEFT JOIN departments d
		ON e.department_id = d.department_id;
```

Includes employees even **if they don’t belong to a department.**

# Running SQL Queries in Python

## Setting Up a Database in Python

```python
import sqlite3
import pandas as pd

# Create a database and connect
conn = sqlite3.connect("company.db")
cursor = conn.cursor()
```

Creates a database named `company.db`.

## Creating a Table in SQL

```python
cursor.execute("""CREATE TABLE employees (
											id INTEGER PRIMARY KEY,
											first_name TEXT,
											last_name TEXT,
											department TEXT,
											salary INTEGER);""")
conn.commit()
```

Creates an `employees` table with 4 columns.

## Inserting Data into the Table

```python
cursor.executemany("""INSERT INTO employees (first_name, last_name, department, salary)
											VALUES (?, ?, ?, ?);
											""", [("Alice", "Johnson", "IT", 70000),
														("Bob", "Smith", "HR", 60000),
														("Charlie", "Brown", "Sales", 50000)])								
conn.commit()							
```

Adds 3 employees to the table.

## Querying Data from Python

```python
df = pd.read_sql_query("SELECT * FROM employees;", conn)
print(df)
```

| `first_name` | `last_name` | `department` | `salary` |
| --- | --- | --- | --- |
| Alice | Johnson | IT | 70000 |
| Bob | Smith | HR | 60000 |
| Charlie | Brown | Sales  | 50000 |

## Using SQL Queries for Analysis

```python
df_high_salary = pd.read_sql_query("SELECT * FROM employees WHERE salary > 60000;", conn)
print(df_high_salary)
```

| `first_name` | `last_name` | `department` | `salary` |
| --- | --- | --- | --- |
| Alice | Johnson | IT | 70000 |

# Practice Problems

## Basic SQL Queries

- Retrieve all employees from the database
- Filter employees in the **IT department.**
- Sort employees by **salary (highest to lowest).**

```python
# Establish connection to SQLite database
conn = sqlite3.connect("company.db")
cursor = conn.cursor()

# Retrieve all employees
df_all_employees = pd.read_sql_query("SELECT * FROM employees;", conn)

# Filter employees in the IT department
df_it_employees = pd.read_sql_query("SELECT * FROM employees WHERE department = 'IT';", conn)

# Sort employees by salary descending
df_sorted_salary = pd.read_sql_query("SELECT * FROM employees ORDER BY salary DESC;", conn)
```

## Aggregation & Grouping

- Count the number of employees in each department
- Find the **average salary per department.**
- Get the **highest salary in the company.**

```python
# Count the number of employees in each department
df_count_per_department = pd.read_sql_query("""
SELECT department, COUNT(*) AS employee_count
FROM employees
GROUP BY department;
""", conn)

# Find the average salary per department
df_avg_salary_per_department = pd.read_sql_query("""
SELECT department, AVG(salary) AS avg_salary
FROM employees
GROUP BY department;
""", conn)

# Get the highest salary in the company
df_highest_salary = pd.read_sql_query("""
SELECT first_name, last_name, salary
FROM employees
ORDER BY salary DESC
LIMIT 1;
""", conn)
```

## Joining Tables

Create a `departments` table and join it with `employees`.

```python
# Creating a departments table
cursor.execute("""
CREATE TABLE IF NOT EXISTS departments (
 department_id INTEGER PRIMARY KEY,
 department_name TEXT
);
""")
conn.commit()

# Inserting departments
cursor.executemany("""
INSERT OR IGNORE INTO departments (department_id, department_name) 
VALUES (?, ?);
""", [(1, "IT"), (2, "HR"), (3, "Sales")])
conn.commit()

# Altering employees table to include department_id
cursor.execute("""
ALTER TABLE employees ADD COLUMN department_id INTEGER;
""")
conn.commit()

# Updating employees with department IDs
cursor.execute("UPDATE employees SET department_id = 1 WHERE department = 'IT';")
cursor.execute("UPDATE employees SET department_id = 2 WHERE department = 'HR';")
cursor.execute("UPDATE employees SET department_id = 3 WHERE department = 'Sales';")
conn.commit()

# Performing an INNER JOIN between employees and departments
df_joined = pd.read_sql_query("""
SELECT employees.first_name, employees.last_name, departments.department_name, employees.salary
FROM employees
INNER JOIN departments ON employees.department_id = departments.department_id;
""", conn)
```

## Python & SQL Integration

- Load SQL query results into a Pandas **DataFrame.**
- Retrieve employees with salaries **above $55,000.**

```python
df_high_salary_python = pd.read_sql_query("SELECT * FROM employees WHERE salary > 65000;", conn)
```