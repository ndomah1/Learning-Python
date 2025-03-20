# 2. Python Basics

# Variables & Data Types

Variables store data values. In Python, you don’t need to declare the type explicitly-Python infers it.

## **Basic Data Types**

| **Data Type** | **Example** |
| --- | --- |
| Integer (`int`) | `x = 10` |
| Float (`float`) | `y = 10.5` |
| String (`str`) | `name = Alice` |
| Boolean (`bool`) | `is_valid = True` |

## **Example: Variable Assignment**

```python
# Assigning different data types
num = 25              # Integer
price = 19.99         # Float
name = "John"         # String
is_available = True   # Boolean

# Print variables
print(num, type(num))
print(price, type(price))
print(name, type(name))
print(is_available, type(is_available))
```

```
25 <class 'int'>
19.99 <class 'float'>
John <class 'str'>
True <class 'bool'>
```

## **Practice Problem**

1. Create three variables:
    1. An integer (`age` with value `27`).
    2. A float (`height` with value `5.9`).
    3. A string (`city` with value `New York`)
2. Print them with their types.
    
    ```python
    age = 27
    height = 5.9
    city = "New York"
    
    print(age, type(age))
    print(height, type(height))
    print(city, type(city))
    ```
    
    ```
    27 <class 'int'>
    5.9 <class 'float'>
    New York <class 'str'>
    ```
    

# Operators

## **Arithmetic Operators**

| **Operator** | Description | Example |
| --- | --- | --- |
| `+` | Addition | `5 + 3 -> 8` |
| `-` | Subtraction | `10 - 4 -> 6` |
| `*` | Multiplication | `2 * 6 -> 12` |
| `/` | Division | `9 / 2 -> 4.5` |
| `//` | Floor Division | `9 // 2 -> 4` |
| `%` | Modulus | `10 % 3 -> 1` |
| `**` | Exponentiation | `2 ** 3 -> 8` |

## **Comparison Operators**

| Operator | Description | Example |
| --- | --- | --- |
| `==` | Equal | `5 == 5 -> True` |
| `!=` | Not Equal | `5 != 3 -> True` |
| `>` | Greater Than | `10 > 5 -> True` |
| `>=` | Greater Than or Equal To | `5 >= 5 -> True` |
| `<` | Less Than | `-2 < 5 -> True` |
| `<=` | Less Than or Equal To | `5 <= 5 -> True` |

**Example:**

```python
a, b = 10, 3
print(a + b)   # Addition
print(a // b)  # Floor division
print(a ** b)  # Exponentiation
print(a >= b)  # Comparison
```

```
13
3
1000
True
```

## **Practice Problem:**

1. Write a Python script that:
    1. Takes two numbers as input.
    2. Prints their sum, difference, product, and quotient.
        
        ```python
        num1 = float(input("Enter the first number: "))
        num2 = float(input("Enter the second number: "))
        
        my_sum = num1 + num2
        my_diff = num1 - num2
        my_prod = num1 * num2
        my_quot = num1 / num2
        
        print(f"{num1} + {num2} = {my_sum}")
        print(f"{num1} - {num2} = {my_diff}")
        print(f"{num1} * {num2} = {my_prod}")
        print(f"{num1} / {num2} = {my_quot}")
        ```
        
        ```
        15 + 4 = 19
        15 * 4 = 11
        15 * 4 =60
        15 / 4 = 3.75
        ```
        

# Control Structures: Conditionals & Loops

## **Conditional Statements (`if`, `elif`, `else`)**

```python
age = 20

if age < 18:
	print("You are a minor.")
elif age , 65:
	print("You are an adult."
else:
	print("You are a senior.")
```

```
You are an adult.
```

## **Loops**

### **For Loop**

```python
for i in range(5):   # Loops from 0 to 4
	print(f"Iteration: {i}")
```

```
Iteration: 0
Iteration: 1
Iteration: 2
Iteration: 3
Iteration: 4
```

### **While Loop**

```python
count = 3

while count > 0:
	print(f"Countdown: {count}")
	count -= 1
```

```
Countdown: 3
Countdown: 2
Countdown: 1
```

## **Practice Problem:**

1. Write a script that:
    1. Takes an integer input.
    2. Uses an `if` statement to check if it’s even or odd.
    3. Uses a `for` loop to print numbers from 1 to the input number.
        
        ```python
        my_num = float(input("Enter a number: "))
        
        if my_num % 2 == 0:
        	print(f"{my_num} is even.")
        else:
        	print(f"{my_num} is odd.")	
        	
        for i in range(1, int(my_num + 1)):
        	print(i)
        ```
        
        ```
        7 is odd.
        1
        2
        3
        4
        5
        6
        7
        ```
        

# Functions

Functions **organize reusable code.**

## Defining & Calling Functions

```python
def greet(name):
	return f"Hello, {name}!"
	
print(greet("Alice"))
```

```
Hello, Alice!
```

## Function with Multiple Arguments

```python
def add(a, b):
	returns a + b
	
result = add(5, 7)
print(f"Sum: {result}")
```

```
Sum: 12
```

## **Practice Problem:**

1. Write a function `calculate_area()` that:
    1. Takes **length** and **width** as parameters.
    2. Returns the area of a rectangle.
    3. Calls the function with values `5, 10` and prints the result.
        
        ```python
        def calculate_area(length, width):
        	return length * width
        	
        result = calculate_area(5, 10)
        print(f"The area is {result} units^2.")
        ```
        
        ```
        The area is 50 units^2.
        ```