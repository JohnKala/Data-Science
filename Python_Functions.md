# 🐍 Python Functions – Condensed Study Notes

---

## 1  |  Why Functions?
- **Encapsulation**: group related statements into a reusable block.  
- **DRY principle**: define once, call many times.  
- **Readability**: meaningful names + doc‑strings act as inline documentation.

---

## 2  |  Anatomy & Syntax  

```python
def function_name(param1, param2=default, *args, **kwargs):
    """Doc‑string explaining purpose."""
    # body
    return value   # optional
```
- Begins with the `def` keyword.  
- **Parameters** can be positional, default, variable‑length (`*args`), or keyword (`**kwargs`).  
- Indentation defines the function body.  
- `return` exits the function and hands back zero → many values.

---

## 3  |  Parameter Types  

| Kind | How to Declare | Example Call |
|------|----------------|--------------|
| Positional | `def f(a, b)` | `f(1, 2)` |
| Default    | `def f(x=10)` | `f()` → uses 10 |
| `*args`    | collects extra **positional** args into a tuple | `f(1, 2, 3)` |
| `**kwargs` | collects extra **keyword** args into a dict | `f(x=1, y=2)` |

➡️ **Order rule**: `positional`, `*args`, *keyword‑only*, `**kwargs`.

---

## 4  |  Return Statement
- `return` with no value → `None`.
- Multiple values are packed into a **tuple** implicitly:

```python
def stats(x, y):
    return x+y, x*y
s, p = stats(3, 4)
```

---

## 5  |  Practical Examples

<details>
<summary>5.1 Even / Odd checker</summary>

```python
def even_or_odd(num):
    """Print whether *num* is even or odd."""
    print("even" if num % 2 == 0 else "odd")
```
</details>

<details>
<summary>5.2 Addition (two params)</summary>

```python
def add(a, b):
    return a + b
```
</details>

<details>
<summary>5.3 Greeting with default parameter</summary>

```python
def greet(name="Guest"):
    print(f"Hello {{name}}, welcome to the paradise!")
```
</details>

<details>
<summary>5.4 Variable‑length demos</summary>

```python
def print_numbers(*args):
    for n in args:
        print(n)

def print_details(*args, **kwargs):
    for v in args:
        print("positional:", v)
    for k, v in kwargs.items():
        print(f"{{k}}: {{v}}")
```
</details>

<details>
<summary>5.5 Multiply with multiple returns</summary>

```python
def multiply(a, b):
    return a * b, a
```
</details>

<details>
<summary>5.6 Temperature converter (°C to °F & vice‑versa)</summary>

```python
def convert_temperature(t, unit):
    """unit: 'C' converts to Fahrenheit, 'F' converts to Celsius"""
    if unit == "C":
        return t * 9/5 + 32
    elif unit == "F":
        return (t - 32) * 5/9
```
</details>

<details>
<summary>5.7 Password strength checker</summary>

```python
def is_strong_password(pw):
    if (len(pw) < 8 or
        not any(c.isdigit() for c in pw) or
        not any(c.islower() for c in pw) or
        not any(c.isupper() for c in pw) or
        not any(c in '!@#$%^&*()_+' for c in pw)):
        return False
    return True
```
</details>

<details>
<summary>5.8 Shopping‑cart total</summary>

```python
def total_cost(cart):
    """cart = [{{'name':..,'price':..,'quantity':..}}, ...]"""
    return sum(item['price']*item['quantity'] for item in cart)
```
</details>

<details>
<summary>5.9 Palindrome test</summary>

```python
def is_palindrome(s):
    s = s.lower().replace(" ", "")
    return s == s[::-1]
```
</details>

<details>
<summary>5.10 Factorial via recursion</summary>

```python
def fact(n):
    return 1 if n == 0 else n * fact(n-1)
```
</details>

<details>
<summary>5.11 Word‑frequency in a file</summary>

```python
def word_freq(path):
    counts = {{}}
    with open(path) as f:
        for line in f:
            for w in line.split():
                w = w.lower().strip('.,!?;:"\'')
                counts[w] = counts.get(w, 0) + 1
    return counts
```
</details>

<details>
<summary>5.12 Email validation (regex)</summary>

```python
import re
_pattern = r'^[A-Za-z0-9_.+-]+@[A-Za-z0-9-]+\.[A-Za-z0-9-.]+$'
def is_valid_email(email):
    return re.match(_pattern, email) is not None
```
</details>

---

## 6  |  Cheat‑Sheet of Handy String Methods
| Method | Purpose |
|--------|---------|
| `str.lower()` / `upper()` | case conversion |
| `str.replace(old, new)` | replace substring |
| `str.strip(chars)` | trim leading/trailing chars |
| `str.isdigit()` | character is 0‑9 |
| `str.islower()` / `isupper()` | case test |

---

### Quick Tips
- Use **doc‑strings** – they surface in `help()` and IDE tooltips.  
- Keep functions **small & single‑purpose**.  
- Prefer returning values rather than printing inside functions (easier to test).  
- Remember the argument order rule when mixing `*args` and `**kwargs`.
