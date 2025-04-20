🐍 Python Tuples: Notes from Udemy Lecture
==========================================

📘 Introduction
---------------

-   Tuples are **ordered** and **immutable** collections in Python.
-   Unlike lists, **tuple elements cannot be changed once assigned**.
-   Tuples support **indexing**, **slicing**, and **common operations**, but with fewer methods.
-   Efficient for:
    -   Representing fixed collections
    -   Function return values
    -   Dictionary keys

* * * * *

🛠 Creating Tuples
------------------

### 🌀 Empty Tuple

```python
empty_tuple = ()
print(empty_tuple)          # ()
print(type(empty_tuple))    # <class 'tuple'>
```
### 📥 Using `tuple()` Constructor

```python
tpl = tuple()
print(type(tpl))  # <class 'tuple'>
```
### 📦 From a List

```python
numbers = tuple([1, 2, 3, 4, 5, 6])
print(numbers)  # (1, 2, 3, 4, 5, 6)
```
### 🔄 Convert Tuple to List

```python
list((1, 2, 3, 4, 5, 6))
```
### 🔀 Mixed Data Types

```python
mixed_tuple = (1, "Hello World", 3.14, True)
print(mixed_tuple)
```
* * * * *

🔍 Accessing Elements
---------------------

```python
print(numbers[0])       # First element
print(numbers[-1])      # Last element
print(numbers[0:4])     # Slicing
print(numbers[::-1])    # Reverse
```
> Tuples support all the indexing/slicing capabilities of lists.

* * * * *

➕ Tuple Operations
------------------

### 🔗 Concatenation

```python
concatenation_tuple = numbers + mixed_tuple
print(concatenation_tuple)
```
### 🔁 Repetition

```python
print(mixed_tuple * 3)
print(numbers * 3)
```
* * * * *

🚫 Tuple Immutability
---------------------

Tuples are **immutable**, meaning elements **cannot be changed**:

```python
numbers[1] = "crash"  # TypeError: 'tuple' object does not support item assignment
```
To modify a tuple:

```python
temp = list(numbers)
temp[1] = "crash"
numbers = tuple(temp)
```
* * * * *

🧰 Common Tuple Methods
-----------------------

### `count()`: Count occurrences

```python
numbers = (1, 2, 3, 4, 5, 6)
print(numbers.count(1))  # 1
```
### `index()`: Return first index of value

```python
print(numbers.index(3))  # 2
```
* * * * *

📦 Packing and Unpacking
------------------------

### Packing

```python
packed_tuple = (1, "hello", 3.14)
print(packed_tuple)
```
### Unpacking

```python
a, b, c = packed_tuple
print(a, b, c)
```
### Starred Unpacking

```python
numbers = (1, 2, 3, 4, 5, 6)
first, *middle, last = numbers
print(first)   # 1
print(middle)  # [2, 3, 4, 5]
print(last)    # 6
```
* * * * *

🧱 Nested Tuples and Lists
--------------------------

### Nested List

```python
nested_list = [
    [1, 2, 3, 4],
    [6, 7, 8, 9],
    [1, 1, "hello", 3.14, 'C']
]
```
Accessing:

```python
print(nested_list[0])         # [1, 2, 3, 4]
print(nested_list[2][2])      # "hello"
print(nested_list[0:3])       # Slicing
```
### Nested Tuple

```python
nested_tuple = ((1, 2, 3), ("A", "B", "C"), (True, False))
print(nested_tuple[1][2])  # "C"
```
### Iterating Over Nested Tuple

```python
for sub_tuple in nested_tuple:
    for item in sub_tuple:
        print(item, end=" ")
```
* * * * *

🧠 Conclusion
-------------

-   Tuples are great when:
    -   You need **immutability**
    -   You want to **store multiple values** in a single variable
    -   You want **hashable elements** for use as dictionary keys
-   Use tuples to make your Python code more **efficient** and **readable**
