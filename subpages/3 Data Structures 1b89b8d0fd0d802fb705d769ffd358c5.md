# 3. Data Structures

Data structures are essential in data analytics for storing and manipulating data efficiently.

# Lists (Ordered, Mutable)

A **list** is an ordered collection that allows duplicate values and can be modified.

## **Creating a List**

```python
# Creating a list
numbers = [10, 20, 30, 40, 50]
fruits = ["apple", "banana", "cherry"]

print(numbers)
print(fruits)
```

```
[10, 20, 30, 40, 50]
['apple', 'banana', 'cherry']
```

## **List Operations**

```python
numbers.append(60)           # Adds 60 to the end
numbers.insert(2, 25)        # Inserts 25 at index 2
numbers.remove(10)           # Removes 10
last_item = numbers.pop()    # Removes last item
sliced_list = numbers[1:4]   # Extracts elements 1 to 3 (excludes index 4)

print(numbers)
print(last_item)
print(sliced_list)
```

```
[20, 25, 30, 40]
50
[25, 30, 40]
```

## **Iterating Over a List**

```python
for fruit in fruits:
	print(fruit)
```

```
apple
banana
cherry
```

# Tuples (Ordered, Immutable)

A **tuple** is like a list but **immutable**, meaning its values cannot be changed after creation.

## **Creating a Tuple**

```python
coordinates = (10.5, 20.3)
person = ("Alice", 25, "Engineer")

print(coordinates)
print(person)
```

```
(10.5, 20.3)
('Alice', 25, 'Engineer')
```

## **Accessing Tuple Elements**

```python
print(person[0])
print(person[-1])
```

```
Alice
Engineer
```

## **Why Use Tuples?**

- Faster than lists.
- Protects data from accidental modification.
- Used as dictionary keys.

# Dictionaries (Key-Value Pairs, Fast Lookups)

A **dictionary** stores data in `{key: value}` pairs, allowing fast lookups.

## **Creating and Accessing a Dictioanry**

```python
person = {"name": "Alice",
					"age": 25,
					"job": "Engineer"}
					
print(person["name"])
print(person.get("age"))
```

```
Alice
25
```

## **Modifying a Dictionary**

```python
person["age"] = 26            # Update age
person["city"] = "New York"   # Add a new key-value pair
del person["job"]             # Remove a key
```

```
{'name': 'Alice', 'age': 26, 'city': 'New York'}
```

## **Iterating Over a Dictionary**

```python
for key, value in person.items():
	print(f"{key}: {value}")
```

```
name: Alice
age: 26
city: New York
```

# Sets (Unordered, Unique Elements)

A **set** is a collection of unique items. It does not allow duplicates and is unordered.

## **Creating a Set**

```python
numbers_set = {1, 2, 3, 4, 5}
duplicate_set = {1, 2, 2, 3, 3, 4}

print(numbers_set)
print(duplicate_set)
```

```
{1, 2, 3, 4, 5}
{1, 2, 3, 4}
```

## **Set Operations**

```python
numbers_set.add(6)      # Adds an element
numbers_set.remove(3)   # Removes an element

print(numbers_set)
```

```python
{1, 2, 4, 5, 6}
```

## **Set Union & Intersection**

```python
A = {1, 2, 3, 4}
B = {3, 4, 5, 6}

print(A | B)  # Union
print(A & B)  # Intersection
```

```
{1, 2, 3, 4, 5, 6}
{3, 4}
```

# **Practice Problems**

## **Lists:**

1. Create a list of five numbers.
2. Append a new number and remove the second element.
3. Print the updated list.

```python
lst = [1, 2, 3, 4, 5]

lst.append(6)
lst.remove(1)
print(lst)
```

```
[1, 3, 4, 5, 6]
```

## **Tuples:**

1. Create a tuple with three elements (name, age, city).
2. Try modifying an element (observe the error).
3. Extract and print the last element.

```python
tple = ("Bruce", 35, "Gotham")

tple[2] = "Metropolis"

print(tple[-1])
```

```
Error message
Gotham
```

## **Dictionaries**

1. Create a dictionary with the keys: `name`, `age`, and `country`.
2. Update the `age`.
3. Add a new key `city` .
4. Print all key-value pairs.

```python
dct = {"name": "Bruce",
			  "age": 35,
				"country": "USA"}
				
dct["age"] = 30
dct["city"] = "Gotham"

for key, value in dct.items():
	print(f"{key}: {value}")
```

```
name: Bruce
age: 30
country: USA
city: Gotham
```

## **Sets:**

1. Create a set of five numbers.
2. Add a duplicate number and print the set (observe that duplicates aren’t added).
3. Perform set union and intersection.

```python
A = {1, 2, 3, 4, 5}

A.add(1)
print(A)

B = {4, 5, 6, 7, 8}

print(A | B)
print(A & B)
```

```
{1, 2, 3, 4, 5}
{1, 2, 3, 4, 5, 6, 7, 8}
{4, 5}
```