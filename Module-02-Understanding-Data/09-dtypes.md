# 🧬 Using `dtypes` in Pandas

> Machine Learning models only understand numbers. If a numeric feature is accidentally stored as a string (`object`), your model training will crash. Checking and fixing data types is a non-negotiable step.

---

# 📖 Table of Contents

1. What is `dtypes`?
2. Common Pandas Data Types
3. Basic Usage
4. Filtering by Data Type
5. Industry Best Practices
6. Interview Questions
7. Summary

---

# 🎯 Learning Objectives

After completing this topic, you will be able to:
- Identify the exact data type of every column using `df.dtypes`.
- Understand the mapping between Python types and Pandas types.
- Select columns dynamically based on their type.

---

# 📘 What is `dtypes`?

`dtypes` is an attribute that returns a Series with the data type of each column.

### Common Pandas Data Types:
- `int64`: Integer numbers (e.g., 25, 100)
- `float64`: Decimal numbers (e.g., 25.5, 3.14)
- `object`: Text/Strings or mixed types (e.g., "Hello", "$500")
- `datetime64`: Dates and Times (e.g., 2023-10-01)
- `bool`: True/False values
- `category`: Categorical data with fixed, limited values (Memory efficient!)

---

# 📂 Basic Usage

```python
import pandas as pd

df = pd.read_csv("employees.csv")

print(df.dtypes)
```

**Output:**
```text
Emp_ID        int64
Name         object
Age           int64
Salary      float64
Is_Active      bool
dtype: object
```

---

# 🔍 Filtering by Data Type

In ML pipelines, you often need to separate numeric columns (to scale them) from categorical columns (to encode them).

```python
# Select only numeric columns
numeric_df = df.select_dtypes(include=['int64', 'float64'])

# Select only categorical/text columns
categorical_df = df.select_dtypes(include=['object'])
```

---

# ⚡ Industry Best Practices

✅ **Verify the "Hidden String" Bug**: If an `Age` column shows up as `object`, it means there is at least one row containing text (like "N/A" or "Unknown"). You must locate and clean these before converting to `int`.
✅ **Optimize with Categories**: If a column like `Department` only has 5 unique text values repeated 10,000 times, convert it from `object` to `category`. This reduces memory usage drastically.

```python
df['Department'] = df['Department'].astype('category')
```

---

# 💼 Interview Questions

### Q1. What does it mean if a numeric column's dtype is `object`?
It means the column contains mixed data types (numbers and strings) or was parsed entirely as strings due to dirty data (like commas in a number).

### Q2. How do you programmatically separate numeric features from categorical features?
By using `df.select_dtypes(include=['number'])` for numerics, and `df.select_dtypes(include=['object', 'category'])` for categoricals.

---

# 📌 Summary

- `dtypes` shows the data type of each column.
- Models require `int64` or `float64`.
- `object` usually means text.
- Use `select_dtypes` for intelligent feature separation.

---

# 🚀 What's Next?

The next topic is:

**[10-memory_usage().md](10-memory_usage().md)**

You will learn how to measure the memory footprint of your DataFrame, an essential skill for Big Data processing.
