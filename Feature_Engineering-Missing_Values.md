
# 🩺 Handling Missing Values in Python (Pandas)  
*Last updated 2025-07-01*  

> **Goal:** Learn *why* data goes missing, *how* to diagnose it, and several hands‑on strategies to fix it – using the Titanic dataset as practice.

---

## 1  Why Missing Values Matter  

Real‑world datasets are almost **never** complete – sensors fail, survey questions are skipped, log files cut short…  
Ignoring the problem can:  

* break model training (`ValueError: Input contains NaN`)  
* bias statistics (means, correlations)  
* waste information if you drop too much data  

---

## 2  Mechanisms of Missingness  

| Acronym | Name | What it means | Example |
|---------|------|---------------|---------|
| **MCAR** | Missing Completely At Random | “Accidental” ✨ — missingness is unrelated to *any* variable (observed or hidden). | Typos during data entry, corrupt sensor packets |
| **MAR** | Missing At Random | Missingness depends **only on other observed variables**. | Survey: income left blank more often by younger respondents |
| **MNAR** | Missing Not At Random | Missingness depends on the **missing value itself** (or unobserved factors). | Employees unsatisfied with pay refuse to report salary |

> *Why care?* The mechanism determines which imputation methods are statistically sound.  
For this tutorial we’ll focus on practical remedies used day‑to‑day.

---

## 3  Imports & Dataset  

```python
import pandas as pd
import numpy as np
import seaborn as sns              # statistical plotting
import matplotlib.pyplot as plt    # base plotting
```

```python
# Titanic passenger data – convenient for demos
df = sns.load_dataset("titanic")
df.head()
```

> **`sns.load_dataset`** grabs small, clean datasets that ship with Seaborn (great for demos).

---

## 4  Diagnosing Missingness  

### 4.1 Quick counts  

```python
df.isna().sum()         # same as .isnull()
```

*Why `.isna()`?* It returns a **boolean mask** (True=missing), so chaining `.sum()` counts True values down each column.

### 4.2 Visual overview *(optional)*  

```python
sns.heatmap(df.isna(), cbar=False)
plt.title("Missing‑value matrix")
plt.show()
```

*(Add the plot to your notebook for an immediate sense of patterns – dark bands signal systematic gaps.)*

---

## 5  Strategy 0 – Deletion (a.k.a. “listwise deletion”)  

```python
df_drop_rows = df.dropna()          # drop rows with *any* NaN
df_drop_cols = df.dropna(axis=1)    # drop columns with *any* NaN
```

| Pros | Cons |
|------|------|
| Fast, no assumptions | Can throw away tons of data & introduce bias |

> **Rule of thumb:** Only drop a column if the *majority* of its entries are missing (e.g. `deck` in Titanic has 77% NaNs).

---

## 6  Strategy 1 – Mean / Median Imputation (Numeric)  

### 6.1 Mean (good for roughly symmetric distributions)

```python
age_mean = df["age"].mean()
df["age_imp_mean"] = df["age"].fillna(age_mean)
```

*Functions explained*  
* **`.mean()`** – arithmetic average (skips NaNs automatically).  
* **`.fillna(value)`** – returns a new Series where NaNs are replaced.

### 6.2 Median (robust to outliers / skew)  

```python
age_median = df["age"].median()
df["age_imp_median"] = df["age"].fillna(age_median)
```

> **Tip:** Use `df["age"].hist()` or `sns.histplot` to inspect distribution shape and decide between mean / median.

---

## 7  Strategy 2 – Mode Imputation (Categorical)  

```python
emb_mode = df["embarked"].mode()[0]   # `.mode()` returns Series
df["embarked_imp"] = df["embarked"].fillna(emb_mode)
```

*Why mode?* Replacing with the **most frequent** class keeps category proportions close to original.

---

## 8  Strategy 3 – Random Sample Imputation  

Keeps the *original distribution* by randomly sampling observed values.

```python
def random_sample_impute(series, seed=None):
    np.random.seed(seed)
    miss_mask = series.isna()
    n_missing = miss_mask.sum()
    samples = np.random.choice(series.dropna(), n_missing, replace=True)
    series.loc[miss_mask] = samples
    return series

df["age_imp_rand"] = random_sample_impute(df["age"].copy(), seed=42)
```

---

## 9  Bonus – Scikit‑Learn Imputers  

| Imputer | When to use |
|---------|-------------|
| `SimpleImputer(strategy="mean/median/most_frequent")` | Same as manual fill but integrates into `Pipeline` |
| `KNNImputer` | Fills NaNs with values from nearest‑neighbour rows |
| `IterativeImputer` | Multivariate regression (MICE) – more advanced |

Small example:

```python
from sklearn.impute import SimpleImputer

num_imputer = SimpleImputer(strategy="median")
df[["age"]] = num_imputer.fit_transform(df[["age"]])
```

---

## 10  Putting It All Together – Mini Workflow  

```python
# 1. Drop columns with >70 % missing
threshold = len(df) * 0.7
df = df.loc[:, df.isna().sum() < threshold]

# 2. Impute numeric & categorical separately
num_cols  = df.select_dtypes("number").columns
cat_cols  = df.select_dtypes("object").columns

df[num_cols] = df[num_cols].apply(
    lambda col: col.fillna(col.median())
)
df[cat_cols] = df[cat_cols].apply(
    lambda col: col.fillna(col.mode()[0])
)
```

---

## 11  Key Take‑Aways  

* Always **profile** missingness first – size & pattern drive the fix.  
* Deleting is easiest but often costly.  
* Mean/median/mode imputation is quick, but injects bias – keep in mind for downstream modelling.  
* For production pipelines use **`sklearn` imputers** inside a `Pipeline` so the same logic applies to training & new data.  

---

### References & Further Reading  

* Little & Rubin – *Statistical Analysis with Missing Data*  
* scikit‑learn documentation: [Imputation](https://scikit-learn.org/stable/modules/impute.html)  

---

*Happy cleaning!* 🧽
