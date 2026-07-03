# 📑 Using `index` in Pandas

> If `columns` represent the features (variables), the `index` represents the records (observations). Understanding the index is crucial for merging datasets and handling time-series data.

---

# 📖 Table of Contents

1. What is the `index`?
2. Default Index (RangeIndex)
3. Setting a Custom Index
4. Resetting the Index
5. Industry Best Practices
6. Summary

---

# 🎯 Learning Objectives

After completing this topic, you will be able to:
- Understand the role of the DataFrame index.
- Set and reset custom indices.
- Understand the performance benefits of a well-defined index.

---

# 📘 What is the `index`?

The `index` is the row label of the DataFrame. 

By default, when you read a CSV without specifying an index, Pandas creates a `RangeIndex` starting from `0` to `n-1`.

---

# 📂 Basic Usage

```python
import pandas as pd

df = pd.read_csv("data.csv")

print(df.index)
```

**Output:**
```text
RangeIndex(start=0, stop=1000, step=1)
```

---

# 🔧 Setting a Custom Index

Often, your dataset already contains a unique identifier (like `Customer_ID` or `Date`). Making this the index makes lookups exponentially faster.

```python
# Set the index to Customer_ID
df = df.set_index("Customer_ID")

print(df.head(2))
```

**Output:**
```text
             Name  Age
Customer_ID           
101           Ram   25
102          John   30
```

*Notice how `Customer_ID` is now separated and acts as the row label.*

---

# 🔄 Resetting the Index

If you manipulate data (like grouping or aggregating), the index can become messy. You can reset it back to a standard numeric column.

```python
# Resets the index, pushing the old index back as a standard column
df = df.reset_index()

# If you want to delete the old index completely
df = df.reset_index(drop=True)
```

---

# ⚡ Industry Best Practices

✅ **Time-Series Models**: In Time-Series forecasting, the `Datetime` column *must* be set as the index. This allows you to resample data (e.g., convert daily data to monthly data).
✅ **Joins/Merges**: When joining massive datasets, joining on indices is computationally faster than joining on standard columns.

---

# 📌 Summary

- `df.index` accesses row labels.
- Use `set_index('col_name')` to use a column as the index.
- Use `reset_index()` to return to a standard numeric `RangeIndex`.

---

# 🚀 What's Next?

The next topic is:

**[09-dtypes.md](09-dtypes.md)**

You will learn how to deeply inspect and manipulate data types, the most common source of bugs in ML pipelines.
