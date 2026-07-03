# 📐 Using `shape` in Pandas

> Data dimensions matter. A dataset with 1,000 rows requires completely different Machine Learning algorithms and hardware than a dataset with 1,000,000,000 rows.

---

# 📖 Table of Contents

1. What is `shape`?
2. Basic Usage
3. Extracting Rows and Columns
4. Industry Best Practices
5. Summary

---

# 🎯 Learning Objectives

After completing this topic, you will be able to:
- Quickly identify dataset dimensions.
- Programmatically extract row and column counts for automated testing.

---

# 📘 What is `shape`?

`shape` is an **attribute** (not a method/function, so no parentheses) of a Pandas DataFrame. It returns a tuple representing the dimensionality of the DataFrame.

Format: `(rows, columns)`

---

# 📂 Basic Usage

```python
import pandas as pd

df = pd.read_csv("customers.csv")

print(df.shape)
```

**Output:**
```text
(15000, 12)
```
This means the dataset has 15,000 rows and 12 columns.

---

# 🧩 Extracting Rows and Columns

Since `shape` returns a tuple, you can access the row count and column count via indexing.

```python
num_rows = df.shape[0]
num_cols = df.shape[1]

print(f"We have {num_rows} records and {num_cols} features.")
```

---

# ⚡ Industry Best Practices

✅ **Use `shape` for Pipeline Validation**: In automated data pipelines, engineers write assertions using `shape`.
```python
# Before merging two datasets
assert df1.shape[0] == df2.shape[0], "Row counts don't match before merge!"
```

✅ **Sanity Check After Filtering**: Always print the `shape` before and after dropping missing values or filtering rows to see exactly how much data you lost.
```python
print("Before drop:", df.shape)
df = df.dropna()
print("After drop:", df.shape)
```

---

# 📌 Summary

- `shape` is an attribute (no `()`).
- Returns `(rows, columns)`.
- Use `shape[0]` for rows and `shape[1]` for columns.

---

# 🚀 What's Next?

The next topic is:

**[07-columns.md](07-columns.md)**

You will learn how to access, clean, and standardize the column names of your DataFrame.
