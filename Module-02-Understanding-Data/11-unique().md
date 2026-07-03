# 🥇 unique() in Pandas

> The `unique()` function identifies all distinct values in a column. It is a critical tool for understanding the variety and exact formatting of your categorical data.

---

# 📖 Table of Contents

1. Introduction
2. Learning Objectives
3. What is `unique()`?
4. Why Do We Use `unique()`?
5. Syntax
6. Parameters
7. Examples
8. Output
9. Industry Example
10. Engineer Thinking
11. Best Practices
12. Common Mistakes
13. Interview Questions
14. Summary
15. Next Topic

---

# 🎯 Learning Objectives

After completing this topic, you will be able to:

- Extract all distinct values from a column.
- Identify dirty data and typos within categories.
- Understand how `unique()` handles missing values (`NaN`).

---

# 📘 What is `unique()`?

The `unique()` function returns an array of all distinct, unique values present in a specific Pandas Series (a single column).

It returns the values in the exact order they first appear in the dataset.

---

# ❓ Why Do We Use `unique()`?

When dealing with categorical features (like City, Department, or Status), you need to know exactly what categories exist before applying Machine Learning encoders (like One-Hot Encoding).

Using `unique()` helps you find data entry errors:
If you expect `['Yes', 'No']`, but `unique()` returns `['Yes', 'No', 'yes', 'NO', 'N/A']`, you instantly know data cleaning is required.

---

# 📝 Syntax

```python
Series.unique()
```
*(Note: `unique()` is called on a specific column/Series, not the entire DataFrame).*

---

# ⚙️ Parameters

The `unique()` function takes **no parameters**.

---

# 💻 Example Dataset

```text
Employee_ID   Department
101           IT
102           HR
103           IT
104           Finance
105           hr
```

---

# 📌 Example 1 – Default Behavior

```python
import pandas as pd

df = pd.read_csv("employees.csv")

print(df['Department'].unique())
```

### Output

```text
['IT' 'HR' 'Finance' 'hr']
```

Notice how it highlights an issue: `'HR'` and `'hr'` are treated as distinct values due to case sensitivity.

---

# 📌 Example 2 – Handling NaNs

```python
import numpy as np

# Adding a missing value
df.loc[5] = [106, np.nan]

print(df['Department'].unique())
```

### Output

```text
['IT' 'HR' 'Finance' 'hr' nan]
```

`unique()` explicitly includes missing values (`NaN`) in the output array, which is very helpful for spotting incomplete columns.

---

# 🏢 Real Industry Example

A Machine Learning Engineer is building a classification model to predict Customer Churn. The target column `Churn_Status` should ideally be binary.

They run:
```python
df['Churn_Status'].unique()
```

Output:
```text
['Churned' 'Active' 'Pending' 'Cancelled' 'Unknown']
```

The engineer realizes the data is not binary. They must work with the business team to map 'Pending' and 'Unknown' into proper categories or drop them before training a binary classification model.

---

# 🧠 Engineer Thinking

When reviewing `unique()`, ask yourself:

- Are there casing typos? (e.g., 'New York' vs 'new york').
- Are there hidden whitespace typos? (e.g., 'Active' vs 'Active ').
- Did `NaN` show up in a column that is supposed to be mandatory?
- Are there too many unique values for One-Hot Encoding?

---

# ⚡ Performance Notes

- `unique()` is heavily optimized and implemented in C under the hood. It is incredibly fast, even on millions of rows.
- It returns a Numpy array, not a Pandas Series.

---

# ✅ Best Practices

- Always run `unique()` on categorical target variables before building classification models.
- If you find casing issues, apply `.str.lower()` or `.str.strip()` to the column and run `unique()` again to verify the fix.

---

# ❌ Common Mistakes

### Mistake 1

Trying to call `unique()` on the entire DataFrame.

```python
# Error!
df.unique()
```
`AttributeError: 'DataFrame' object has no attribute 'unique'`. It must be called on a specific column (Series).

---

### Mistake 2

Assuming the output is sorted.

`unique()` returns values in order of appearance, not alphabetically.

---

# 💼 Interview Questions

### Q1. Does `unique()` include missing values (`NaN`)?

Yes, `NaN` will be included in the output array if it exists in the column.

---

### Q2. What data type does `unique()` return?

It returns a NumPy array (`ndarray`).

---

### Q3. Why do 'Yes' and 'yes' show up as two distinct values?

Because `unique()` is strictly case-sensitive. String normalization is required to merge them.

---

# 📌 Summary

- `unique()` extracts distinct values from a specific column.
- It is crucial for detecting typos and case-sensitivity issues in categorical data.
- It must be called on a Series, not a DataFrame.
- It includes `NaN` values.

---

# 🚀 Next Topic

The next topic is:

**12-nunique().md**

You'll learn how to quickly count the number of unique values, which is essential for determining feature cardinality.
