
# 🚰 `filter()` Function in Python — Handy Guide  

*Last updated: 2025-06-23*

---

## 1  |  Why `filter()`?

> **`filter(func, iterable)`**  
> Builds an **iterator** containing only the elements for which `func(element)` is **truthy**.

- Great for **screening / cleaning** data.  
- Works with any iterable (lists, tuples, sets, dict‑views, generators…).  
- Because it yields a **lazy** iterator, it’s memory‑efficient; convert with `list()` when you need the results right away.

---

## 2  |  Basic Pattern  

```python
def keep_if(x):
    return ...  # True / False

result_iter = filter(keep_if, iterable)
result_list = list(result_iter)   # materialise
```

---

## 3  |  Starter Example — Even Numbers

```python
def is_even(n):
    return n % 2 == 0

nums   = [1,2,3,4,5,6,7,8]
evens  = list(filter(is_even, nums))
print(evens)          # ➜ [2, 4, 6, 8]
```

---

## 4  |  Lambda + `filter()` (One‑Liner)

```python
nums  = [1,2,3,4,5,6,7,8,9]
gt5   = list(filter(lambda x: x > 5, nums))
# [6, 7, 8, 9]
```

---

## 5  |  Multiple Conditions

```python
nums = [1,2,3,4,5,6,7,8,9]
even_and_gt5 = list(
    filter(lambda x: x > 5 and x % 2 == 0, nums)
)
# [6, 8]
```

(Combine with `and / or` for complex rules.)

---

## 6  |  Filtering Dictionaries (List of Objects)

```python
people = [
    { "name": "Krish", "age": 32 },
    { "name": "Jack",  "age": 33 },
    { "name": "John",  "age": 25 },
]

older = list(filter(lambda p: p["age"] > 25, people))
# [{'name': 'Krish', 'age': 32}, {'name': 'Jack', 'age': 33}]
```

---

## 7  |  Quick Trick — Remove “Falsy” Items

When `func` is **`None`**, `filter()` keeps elements that are *truthy* by default.

```python
raw = ["apple", "", None, "banana", 0, "cherry"]
clean = list(filter(None, raw))
# ['apple', 'banana', 'cherry']
```

(Handy for stripping blanks or zeroes.)

---

## 8  |  Common Pitfalls

| Mistake | Fix |
|---------|-----|
| Calling the function: `filter(is_even(), nums)` | Pass **function obj**: `filter(is_even, nums)` |
| Forgetting to consume iterator | `list(filter(...))` or iterate |
| Expecting transformed values (e.g., squares) | Use `map()` or comprehension; `filter()` only selects |

---

## 9  |  `filter()` vs. List‑Comprehension

| Goal | List‑Comprehension | `filter()` |
|------|--------------------|------------|
| Simple keep‑rule | `[x for x in nums if x > 5]` | `list(filter(lambda x: x > 5, nums))` |
| Needs transform too | `[x**2 for x in nums if x>5]` | chain `map()` after `filter()` |

Choose the one that reads clearer.

---

## 🔖 Cheat‑Sheet Snippets

```python
# Keep positive numbers
positive = list(filter(lambda n: n > 0, data))

# Keep strings longer than 3
longs = list(filter(lambda s: len(s) > 3, words))

# Keep dicts missing a field
incomplete = list(filter(lambda d: "id" not in d, records))
```

---

### TL;DR

- `filter()` keeps, `map()` transforms.  
- Pass **callables** (named or lambda) + iterable(s).  
- Remember it’s **lazy** — wrap with `list()` for instant results.

Clean data, happy code! 🧹
