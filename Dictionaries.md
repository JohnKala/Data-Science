📘 Dictionaries in Python: Comprehensive Notes
----------------------------------------------

### 🔹 Overview

Topics covered:

1.  Introduction to dictionaries

2.  Creating dictionaries

3.  Accessing elements

4.  Modifying elements

5.  Common methods

6.  Iterating through dictionaries

7.  Nested dictionaries

8.  Dictionary comprehension

9.  Practical examples

* * * * *

### 📌 1. Introduction to Dictionaries

-   A **dictionary** is an **unordered** collection of **key-value pairs**.

-   **Keys** must be:

    -   Unique

    -   Immutable (e.g., strings, numbers, tuples)

-   **Values** can be any Python object.

* * * * *

### 🛠️ 2. Creating Dictionaries

python

CopyEdit

`# Using curly braces
empty_dict = {}
print(type(empty_dict))  # Output: <class 'dict'>

# Using dict() constructor
empty_dict = dict()`

Creating a populated dictionary:

python

CopyEdit

`student = {
    "name": "Krish",
    "age": 32,
    "grade": 24
}
print(student)`

If duplicate keys are provided, the last one will overwrite the previous:

python

CopyEdit

`student = {"name": "Krish", "age": 32, "name": 24}
print(student)  # name: 24`

* * * * *

### 🔍 3. Accessing Dictionary Elements

python

CopyEdit

`student = {"name": "Krish", "age": 32, "grade": "A"}

# Direct access
print(student["grade"])  # Output: A

# Using get()
print(student.get("grade"))  # Output: A
print(student.get("last_name"))  # Output: None
print(student.get("last_name", "Not Available"))  # Output: Not Available`

* * * * *

### ✏️ 4. Modifying Dictionary Elements

-   Dictionaries are **mutable**.

-   You can **update**, **add**, or **delete** elements.

python

CopyEdit

`# Update
student["age"] = 33

# Add
student["address"] = "India"

# Delete
del student["grade"]`

* * * * *

### 🧰 5. Dictionary Methods

python

CopyEdit

`student = {"name": "Krish", "age": 33, "address": "India"}

# Get all keys
print(student.keys())

# Get all values
print(student.values())

# Get all items
print(student.items())`

* * * * *

### 🧠 6. Shallow Copy vs Direct Assignment

python

CopyEdit

`# Direct assignment creates a reference
student_copy = student
student["name"] = "Krish 2"
print(student_copy["name"])  # Output: Krish 2 (same memory reference)

# Shallow copy creates a new object
student_copy_1 = student.copy()
student["name"] = "Krish 3"
print(student_copy_1["name"])  # Output: Krish 2`

* * * * *

### 🔁 7. Iterating Over Dictionaries

python

CopyEdit

`# Over keys
for key in student.keys():
    print(key)

# Over values
for value in student.values():
    print(value)

# Over key-value pairs
for key, value in student.items():
    print(f"{key}: {value}")`

* * * * *

### 🧩 8. Nested Dictionaries

python

CopyEdit

`students = {
    "student1": {"name": "Krish", "age": 32},
    "student2": {"name": "Peter", "age": 35}
}

# Access nested value
print(students["student2"]["age"])  # Output: 35

# Iterating
for student_id, student_info in students.items():
    print(f"ID: {student_id}")
    for key, value in student_info.items():
        print(f"{key}: {value}")`

* * * * *

### 🧮 9. Dictionary Comprehension

python

CopyEdit

`# Simple example
squares = {x: x**2 for x in range(5)}

# Conditional comprehension (even numbers)
even_squares = {x: x**2 for x in range(10) if x % 2 == 0}`

* * * * *

### ✅ 10. Practical Examples

#### Count frequency of elements in a list

python

CopyEdit

`numbers = [1,2,2,3,3,3,4,4,4,4]
frequency = {}

for number in numbers:
    if number in frequency:
        frequency[number] += 1
    else:
        frequency[number] = 1

print(frequency)  # Output: {1: 1, 2: 2, 3: 3, 4: 4}`

#### Merging Dictionaries

python

CopyEdit

`dict1 = {'a': 1, 'b': 2}
dict2 = {'b': 3, 'c': 4}

# Merging using **
merged_dict = {**dict1, **dict2}
print(merged_dict)  # Output: {'a': 1, 'b': 3, 'c': 4}`

* * * * *
