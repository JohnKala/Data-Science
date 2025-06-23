# ⚡️ Lambda Functions in Python – Quick Reference

---

## 1  |  What Is a Lambda?
> A **lambda** (a.k.a. *anonymous*) function is a **single‑expression** function declared with the `lambda` keyword—no `def`, no name.

```python
lambda arguments: expression
```

- **Anonymous** → function object assigned to a variable or passed directly.  
- Accepts **any number** of arguments but **exactly one** expression (which becomes the return value).  
- Ideal for short, throw‑away logic or as a callback for *higher‑order* functions like `map`, `filter`, `sorted`, etc.

---

## 2  |  Basic Conversions

| Traditional `def` | Equivalent Lambda |
|-------------------|-------------------|
|```python\ndef add(a, b):\n    return a + b```|```python\nadd = lambda a, b: a + b```|
|```python\ndef is_even(n):\n    return n % 2 == 0```|```python\nis_even = lambda n: n % 2 == 0```|
|```python\ndef total(x, y, z):\n    return x + y + z```|```python\ntotal = lambda x, y, z: x + y + z```|

> **Remember** – keep it simple. If logic needs `if/else`, loops, or multiple statements, stick with a normal `def`.

---

## 3  |  Calling a Lambda

```python
add = lambda a, b: a + b
result = add(5, 6)       # ➜ 11
```

Internally, lambdas are just functions:

```python
type(add)  # <class 'function'>
```

---

## 4  |  Lambdas with `map` & `filter`

### 4.1 `map(function, iterable)` → applies `function` to each element

```python
nums = [1, 2, 3, 4, 5, 6]
squares = list(map(lambda x: x**2, nums))
# [1, 4, 9, 16, 25, 36]
```

### 4.2 `filter(function, iterable)` → keeps elements where function returns **True**

```python
evens = list(filter(lambda x: x % 2 == 0, nums))
# [2, 4, 6]
```

*(The function argument can be any callable—lambdas just keep it concise.)*

---

## 5  |  Real‑World Mini‑Examples

| Task | Lambda + Higher Order |
|------|----------------------|
| **Sort names by last char** |```python\nnames.sort(key=lambda s: s[-1])``` |
| **Convert °C list to °F** |```python\nc_to_f = list(map(lambda c: c*9/5+32, temps_c))``` |
| **Remove blanks from list** |```python\nclean = list(filter(lambda s: s.strip(), items))``` |

---

## 6  |  Pros & Cons

### ✅ When to Use
- One‑liner transformations or predicates.
- As quick *key* / *func* arguments (`sorted`, `map`, GUI callbacks).
- Avoiding clutter for throw‑away logic.

### ⚠️ When **Not** to Use
- Anything needing statements (`for`, `if`, `try`).
- Complex business logic (hurts readability & debuggability).
- When a descriptive `def` name would **clarify intent**.

---

## 7  |  Cheat‑Sheet

| Snippet | What it does |
|---------|--------------|
|`lambda _: None`| throws away input, returns `None`|
|`lambda *args: sum(args)`| variable args to sum|
|`lambda s: s.lower().strip()`| quick text normalizer|
|`sorted(data, key=lambda t: t[1])`| sort by 2nd tuple item|

---

### Quick Tips for Beginners
1. Think of a lambda as **`return <expression>`**—no need to write `return`.
2. Test your expression in a normal function first; convert to lambda once it’s rock solid.
3. Use descriptive variable names for the **arguments** so the expression stays readable.

Happy concise coding! 🙌
