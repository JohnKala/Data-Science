
# 🏋️‍♂️ Handling Imbalanced Classification Datasets in Python  
*Last updated 2025-07-01*  

A common headache in real‑world machine‑learning is that one class *vastly* outnumbers the other(s).  
If you feed such data straight into a model, it tends to **memorise the majority class** and ignore the rest – resulting in (misleadingly) high accuracy but poor real‑world performance.

This note (an expanded, beginner‑friendly version of the original notebook) shows how to:

1. **Create** a deliberately imbalanced toy dataset (so results are predictable).  
2. **Diagnose** the imbalance visually and numerically.  
3. **Fix** it with two classic techniques: **upsampling** (a.k.a. minority over‑sampling) and **downsampling** (a.k.a. majority under‑sampling).  
4. Discuss pros & cons and common pitfalls.

---

## 0  Imports & Setup  

```python
import numpy as np                 # numerical arrays
import pandas as pd                # tabular data
import seaborn as sns              # quick plots
import matplotlib.pyplot as plt    # base plotting

from sklearn.utils import resample # handy re‑sampling helper

# so that our random numbers reproduce identically every run
np.random.seed(42)
```

### ‑‑ What each library is for?

| Library | Purpose (one‑liner) |
|---------|--------------------|
| **NumPy** (`np`) | Fast maths on arrays / vectors (think Excel cells on steroids). |
| **Pandas** (`pd`) | Spreadsheet‑like “DataFrame” for cleaning, slicing, grouping. |
| **Seaborn** (`sns`) | Prettier statistical charts built on Matplotlib. |
| **Matplotlib** (`plt`) | Low‑level plotting library; Seaborn sits on top. |
| **`sklearn.utils.resample`** | Simple function for bootstrapping / up‑ or down‑sampling rows. |

---

## 1  Build a Toy Imbalanced Dataset  

We’ll mimic a binary‑classification problem with **1 000** rows, but make the target variable heavily skewed (90 % vs 10 %).

```python
N_SAMPLES      = 1_000             # total rows
MAJORITY_PROP  = 0.90              # 90 % zeros
MINORITY_PROP  = 1 - MAJORITY_PROP

n_majority = int(N_SAMPLES * MAJORITY_PROP)   # 900
n_minority = N_SAMPLES - n_majority           # 100

# --- feature matrix (2 numeric columns) ------------------------------
feat_majority = pd.DataFrame({
    "feature1": np.random.normal(loc=0.0,  scale=1.0,  size=n_majority),
    "feature2": np.random.normal(loc=0.25, scale=1.2,  size=n_majority),
    "target":   0                                   # majority label
})

feat_minority = pd.DataFrame({
    "feature1": np.random.normal(loc=2.5,  scale=1.1,  size=n_minority),
    "feature2": np.random.normal(loc=-1.0, scale=0.9,  size=n_minority),
    "target":   1                                   # minority label
})

df = pd.concat([feat_majority, feat_minority]).reset_index(drop=True)
```

### What does each line do?

* `np.random.normal(loc, scale, size)` – draws random numbers from a *Normal* (Gaussian) distribution with a chosen mean (`loc`) and standard deviation (`scale`).  
* `pd.DataFrame({...})` – creates a spreadsheet‑like table from dicts of column‑name ➜ arrays.  
* `pd.concat([...]).reset_index()` – sticks the two tables together (row‑wise) and rebuilds a clean 0…N row index.

```python
df.head()
```

> ```
>    feature1  feature2  target
> 0  0.496714  1.389578       0
> 1 -0.138264  1.158060       0
> 2  0.647689  0.573416       0
> 3  1.523030  0.552974       0
> 4 -0.234153 -0.199355       0
> ```

---

### 1.1 Quick imbalance check  

```python
df["target"].value_counts()
```
> ```
> 0    900
> 1    100
> Name: target, dtype: int64
> ```

Or visualise:

```python
sns.countplot(x="target", data=df)
plt.title("Class distribution before balancing")
plt.show()
```

*(Add image to repo if you like; it will show a tall bar for class 0 and a tiny one for class 1.)*

---

## 2  Technique A – **Upsampling** (Minority Over‑Sampling)  

Idea: **duplicate** or *bootstrap* minority rows until both classes have equal counts.

### 2.1 Split majority / minority subsets  

```python
df_minority = df[df["target"] == 1]
df_majority = df[df["target"] == 0]
```

### 2.2 Resample minority set *with replacement*  

```python
df_minority_upsampled = resample(
    df_minority,
    replace=True,                   # sample with replacement  🔁
    n_samples=len(df_majority),     # up to 900 rows
    random_state=42                 # reproducible
)
```

### 2.3 Combine back

```python
df_upsampled = pd.concat([df_majority, df_minority_upsampled]).reset_index(drop=True)
```

Quick check:

```python
df_upsampled["target"].value_counts()
```
> ```
> 0    900
> 1    900
> ```

---

## 3  Technique B – **Downsampling** (Majority Under‑Sampling)  

Idea: **discard** random majority rows until they match the minority count.

```python
df_majority_down = resample(
    df_majority,
    replace=False,                  # no duplicates
    n_samples=len(df_minority),     # down to 100 rows
    random_state=42
)

df_downsampled = pd.concat([df_majority_down, df_minority]).reset_index(drop=True)
df_downsampled["target"].value_counts()
```
> ```
> 0    100
> 1    100
> ```

---

## 4  Compare Strategies  

| | Upsampling | Downsampling |
|---|-----------|-------------|
| Keeps *all* minority info | ✅ | ✅ |
| Keeps majority info | ✅ (but duplicated) | ❌ |
| Risk of over‑fitting | Higher | Lower |
| Risk of under‑fitting | Lower | Higher |
| When to prefer | Small datasets | Huge datasets |

---

## 5  Visual Check  

```python
fig, axes = plt.subplots(1, 2, figsize=(10,4))
sns.countplot(x="target", data=df_upsampled,  ax=axes[0]).set_title("Upsampled")
sns.countplot(x="target", data=df_downsampled, ax=axes[1]).set_title("Downsampled")
plt.suptitle("Balanced class counts")
plt.show()
```

---

## 6  Next Steps & Tips  

* Evaluate with **precision/recall or F1**, not raw accuracy.  
* Put samplers inside a **`sklearn.pipeline.Pipeline`** so the same logic is applied during training & when serving the model.  
* Explore smarter methods from **`imbalanced-learn`**: `SMOTE`, `ADASYN`, `TomekLinks`, etc.

### Quick SMOTE example

```python
from imblearn.over_sampling import SMOTE
smote = SMOTE(random_state=42)
X_balanced, y_balanced = smote.fit_resample(df[["feature1", "feature2"]], df["target"])
```

---

## 7  Common Beginner Pitfalls  

* Trusting accuracy on skewed data (“accuracy paradox”).  
* Forgetting to shuffle after resampling – can leak ordering patterns into model.  
* Testing on data that has been resampled (always keep *test* distribution untouched!).

---

### Further Reading  

* scikit‑learn docs – <https://scikit-learn.org/stable/modules/impute.html>  
* imbalanced‑learn docs – <https://imbalanced-learn.org/stable/>  
* Blog post: **“Accuracy Paradox”** (search online)

---

*Happy balancing!* ⚖️
