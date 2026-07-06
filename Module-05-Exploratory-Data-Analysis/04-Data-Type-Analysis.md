# 🧬 Data Type Analysis

> Analyzing data types is a fundamental EDA step. Models require specific types to function—numeric for regression, categorical for classification mapping. Data Type Analysis ensures your columns are what they claim to be.

---

# 📖 Table of Contents

1. Introduction
2. Learning Objectives
3. What is Data Type Analysis?
4. Why Do We Use It?
5. Syntax (`dtypes`, `info`, `select_dtypes`)
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

- Quickly identify the datatype of every column using `dtypes`.
- View memory usage and null counts alongside types using `info()`.
- Dynamically split your dataset into numeric and categorical features using `select_dtypes()`.

---

# 📘 What is Data Type Analysis?

Data Type Analysis is the process of auditing a DataFrame to confirm that integers are `int64`, decimals are `float64`, text is `object` or `category`, and dates are `datetime64`.

---

# ❓ Why Do We Use It?

In an automated Machine Learning pipeline, you apply scaling to numerical data and encoding to categorical data. If a numerical column accidentally slips in as an `object` (because of a single comma or dollar sign), the pipeline will encode it instead of scaling it, destroying the mathematical relationships in the data.

---

# 📝 Syntax

```python
# View data types
df.dtypes

# View full technical summary
df.info()

# Filter DataFrame by data type
df.select_dtypes(include=None, exclude=None)
```

---

# ⚙️ Parameters

For `select_dtypes()`:

| Parameter | Description | Default |
|-----------|-------------|---------|
| `include` | List of types to include (e.g., `['number']` or `['object']`). | `None` |
| `exclude` | List of types to exclude. | `None` |

---

# 💻 Example Dataset

```text
ID       Name      Age      Salary       Join_Date
1        Ram       25       50000        2023-01-01
2        John      30       $60000       2023-02-01
```

---

# 📌 Example 1 – Detecting Hidden Bugs with `dtypes`

```python
import pandas as pd

df = pd.read_csv('data.csv')
print(df.dtypes)
```

### Output
```text
ID            int64
Name         object
Age           int64
Salary       object  <-- BUG! Should be numeric.
Join_Date    object  <-- BUG! Should be datetime.
dtype: object
```

---

# 📌 Example 2 – Full Technical Audit with `info()`

```python
df.info()
```
This shows the `dtypes`, the non-null count (to spot missing data), and the memory usage footprint in one shot.

---

# 📌 Example 3 – Dynamic Feature Selection

Instead of hardcoding column names, modern ML pipelines use `select_dtypes` to grab columns dynamically.

```python
# Grab all numeric columns for scaling
num_df = df.select_dtypes(include=['number'])

# Grab all categorical columns for One-Hot Encoding
cat_df = df.select_dtypes(include=['object', 'category'])
```

---

# 🏢 Real Industry Example

An MLOps engineer is building a robust Random Forest pipeline. The input dataset changes daily; sometimes it has 20 numeric columns, sometimes 25. 

By using `df.select_dtypes(include=['number'])`, the pipeline automatically adapts to the incoming schema and scales the correct columns without the engineer having to update a hardcoded list of names every morning.

---

# 🧠 Engineer Thinking

When auditing data types, ask yourself:

- Did my dates load as `object` strings? (They almost always do, necessitating a `pd.to_datetime()` fix).
- Is there a column typed as `object` that I know for a fact should be numeric? (Time to search for dirty text like "N/A" or symbols).
- Can I convert repetitive `object` columns to `category` to save RAM?

---

# ⚡ Performance Notes

- `select_dtypes` creates a view/copy of the data very quickly and is heavily optimized.

---

# ✅ Best Practices

- Always use `select_dtypes` in production pipelines instead of manually passing lists of column names.
- Always check `info()` immediately after reading a CSV file.

---

# ❌ Common Mistakes

### Mistake 1
Assuming `object` strictly means "String". In Pandas, `object` is a catch-all. If a column has integers, floats, lists, and strings all mixed together, it will be labeled `object`.

---

# 💼 Interview Questions

### Q1. How do you separate numeric features from text features programmatically in Pandas?
By using `df.select_dtypes(include=['number'])` for numeric and `include=['object']` for text.

### Q2. What does `df.info()` provide that `df.dtypes` does not?
`info()` provides the total row count, non-null counts per column (for missing data detection), and total memory usage.

---

# 📌 Summary

- `dtypes` and `info()` are diagnostic tools to ensure data schema integrity.
- Unexpected `object` types usually indicate dirty, mixed data.
- `select_dtypes()` is the industry standard for routing columns in automated ML pipelines.

---

# 🚀 Next Topic

The next topic is:

**05-Categorical-Analysis.md**

You'll dive into analyzing text and categories using `unique()`, `nunique()`, and `value_counts()`.
