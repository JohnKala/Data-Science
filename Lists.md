Python Lists: Notes from Udemy Lecture
======================================

📘 Introduction
---------------

-   Lists are **ordered**, **mutable** collections of items.
-   They allow **different data types** within a single list.
-   Powerful due to:
    -   Index-based access
    -   Built-in methods for modification
    -   Flexibility for nesting, comprehension, and iteration

* * * * *

🛠 Creating Lists
-----------------

```python
lst = []
print(type(lst))  # <class 'list'>
```
### Examples:

```python
names = ["Krish", "Jack", "Jacob", 1, 2, 3, 4, 5]
mixed_list = [1, "Hello", 3.14, True]
print(names)
print(mixed_list)
```
* * * * *

🔍 Accessing List Elements
--------------------------

```python
fruits = ["apple", "banana", "cherry", "kiwi", "guava"]
print(fruits[0])   # "apple"
print(fruits[2])   # "cherry"
print(fruits[4])   # "guava"
print(fruits[-1])  # last element: "guava"
```
### Slicing

```python
print(fruits[1:])     # ["banana", "cherry", "kiwi", "guava"]
print(fruits[1:3])    # ["banana", "cherry"]
print(fruits[::2])    # ["apple", "cherry", "guava"]
print(fruits[::-1])   # Reversed list
```
* * * * *

✏️ Modifying List Elements
--------------------------

```python
fruits[1] = "watermelon"
print(fruits)
```
Be careful when replacing with strings:

```python
fruits[1:] = "orange"  # List will interpret this as individual characters
```
* * * * *

🧰 List Methods
---------------

### `append()`

```python
fruits.append("orange")`
```
### `insert(index, value)`

```python
fruits.insert(1, "watermelon")
```
### `remove(value)`

```python
fruits.remove("banana")  # removes first occurrence
```
### `pop()`

```python
last_fruit = fruits.pop()
print(last_fruit)  # "orange"
```

### `index(value)`

```python
idx = fruits.index("cherry")  # returns index
```

### `count(value)`

```python
fruits.count("banana")
```

### `sort()` and `reverse()`

```python
fruits.sort()     # ascending order
fruits.reverse()  # reverse the list
```

### `clear()`

```python
fruits.clear()    # removes all elements
```

* * * * *

🔪 Advanced Slicing
-------------------

```python
numbers = [1,2,3,4,5,6,7,8,9,10]
print(numbers[2:5])      # [3,4,5]
print(numbers[5:])       # [6,7,8,9,10]
print(numbers[::2])      # Step size of 2
print(numbers[::-1])     # Reversed list
print(numbers[::-2])     # Reversed with step 2
```

* * * * *

🔁 Iterating Over Lists
-----------------------

### Basic

```python
for number in numbers:
    print(number)
```

### With Index

```python
for idx, val in enumerate(numbers):
    print(idx, val)
```

* * * * *

🧠 List Comprehension
---------------------

### 📘 Syntax

```python
[expression for item in iterable]
[expression for item in iterable if condition]
```

### 🔢 Example: Squares

```python
[x**2 for x in range(10)]
```

### 🧮 Example: Even Numbers

```python
[num for num in range(10) if num % 2 == 0]
```

### 🧱 Nested List Comprehension

```python
list1 = [1, 2, 3, 4]
list2 = ['a', 'b', 'c', 'd']
pairs = [(i, j) for i in list1 for j in list2]
```

### 🔧 With Functions

```python
words = ["hello", "world", "python", "list", "comprehension"]
[length for length in map(len, words)]
```

* * * * *

📍 Conclusion
-------------

-   Lists are one of Python's most versatile data structures.
-   Understanding **indexing**, **methods**, **slicing**, and **comprehension** is essential.
-   Practicing list operations is key to mastering Python.
