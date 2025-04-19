Python Sets: Notes from Udemy Lecture
=====================================

📘 Introduction
---------------
-   Sets are **built-in data types** in Python.
-   Used to store **collections of unique items**.
-   **Unordered** (no indexing) and **no duplicates allowed**.
-   Useful for:
    -   Membership testing
    -   Removing duplicates
    -   Performing set operations (union, intersection, etc.)

* * * * *

🛠 Creating Sets
----------------

```python
my_set = {1, 2, 3, 4, 5}
print(my_set)
print(type(my_set))  # <class 'set'>
```

### 🌀 Empty Set

```python
my_empty_set = set()
print(type(my_empty_set))  # <class 'set'>
```

### 📥 From Lists or Tuples

```python
my_set = set([1, 2, 3, 4, 5, 6])
print(my_set)
```

🔁 **Duplicates are automatically removed:**

```python
my_set = set([1, 2, 3, 4, 5, 6, 5, 6])
print(my_set)  # {1, 2, 3, 4, 5, 6}
```

* * * * *

🔧 Basic Set Operations
-----------------------

### ➕ Adding Elements

```python
my_set.add(7)
print(my_set)
```

Adding a duplicate does nothing:

```python
my_set.add(7)
print(my_set)  # No change
```

### ➖ Removing Elements

```python
my_set.remove(3)  # Raises KeyError if 3 not present
```

```python
my_set.discard(10)  # No error if element is absent`
```
### 🎲 Popping Elements (Removes a random element)

```python
removed = my_set.pop()
print(removed)
print(my_set)
```

### 🧹 Clearing All Elements

```python
my_set.clear()
print(my_set)  # set()
```
* * * * *

🧪 Membership Testing
---------------------

```python
3 in my_set  # True
10 in my_set  # False
```
* * * * *

➗ Mathematical Set Operations
-----------------------------

```python
set1 = {1, 2, 3, 4, 5, 6}
set2 = {4, 5, 6, 7, 8, 9}
```

### 🔗 Union

```python
set1.union(set2)
```

### 🔀 Intersection

```python
set1.intersection(set2)
```

### 🔄 Intersection Update

```python
set1.intersection_update(set2)
```
### ➖ Difference

```python
set1.difference(set2)
```

### 🔁 Difference Update

```python
set1.difference_update(set2)
```

### 🪞 Symmetric Difference (unique elements from both sets)

```python
set1.symmetric_difference(set2)
```
* * * * *

🧮 Subset & Superset
--------------------

```python
set1.issubset(set2)
set1.issuperset(set2)
```
* * * * *

🧑‍💻 Use Cases
---------------

### 🚿 Removing Duplicates from a List

```python
my_list = [1, 2, 2, 3, 4, 4, 5]
unique_items = set(my_list)
print(unique_items)`
```
### 📊 Counting Unique Words in Text

```python
text = "In this tutorial we are discussing about sets"
words = text.split()
unique_words = set(words)
print(unique_words)
print("Count:", len(unique_words))
```
