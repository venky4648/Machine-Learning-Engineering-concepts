# ℹ️ info() in Pandas

> The `info()` function is used to print a concise summary of a DataFrame. It helps engineers inspect the overall structure, including column names, data types, non-null counts, and memory usage, making it an essential diagnostic tool.

---

# 📖 Table of Contents

1. Introduction
2. Learning Objectives
3. What is `info()`?
4. Why Do We Use `info()`?
5. Syntax
6. Parameters
7. Example Dataset
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

- Understand the purpose of `info()`.
- Inspect the structure and schema of a dataset.
- Identify missing values quickly via non-null counts.
- Check column data types for consistency.
- Monitor memory usage of a dataset.

---

# 📘 What is `info()`?

The `info()` function prints a concise summary of a DataFrame.

It provides details such as:

- Total number of rows and column range.
- Column names.
- Number of non-null values per column.
- Data types (dtypes) of columns.
- Estimated memory usage.

It is a high-level "health check" for your data.

---

# ❓ Why Do We Use `info()`?

When working with real-world data, you cannot assume the data is clean. 

Using `info()` helps you quickly identify:

- **Missing Data**: If you have 10,000 rows but a column shows 9,000 non-null values, 1,000 are missing.
- **Incorrect Types**: If a `Salary` column shows up as `object` (text) instead of numeric, there is a formatting issue.
- **Memory Overhead**: For large datasets, checking memory consumption ensures your environment won't crash.

---

# 📝 Syntax

```python
DataFrame.info(
    verbose=None,
    buf=None,
    max_cols=None,
    memory_usage=None,
    show_counts=None
)
```

---

# ⚙️ Parameters

| Parameter | Description | Default |
|-----------|-------------|---------|
| `verbose` | Whether to print the full summary | `True` |
| `max_cols` | Maximum number of columns to print | Configuration dependent |
| `memory_usage` | Specifies if memory usage should be displayed | `True` |
| `show_counts` | Whether to show non-null counts | `True` |

---

# 💻 Example Dataset

```text
Employee_ID   Name      Age   Department   Salary
101           Ram       25    IT           50000
102           Ravi      28    HR           60000
103           John      NaN   Finance      70000
104           Priya     24    IT           NaN
105           Anjali    27    Sales        52000
```

---

# 📌 Example 1 – Default Behavior

```python
import pandas as pd

df = pd.read_csv("employees.csv")

df.info()
```

### Output

```text
<class 'pandas.core.frame.DataFrame'>
RangeIndex: 5 entries, 0 to 4
Data columns (total 5 columns):
 #   Column       Non-Null Count  Dtype  
---  ------       --------------  -----  
 0   Employee_ID  5 non-null      int64  
 1   Name         5 non-null      object 
 2   Age          4 non-null      float64
 3   Department   5 non-null      object 
 4   Salary       4 non-null      float64
dtypes: float64(2), int64(1), object(2)
memory usage: 328.0+ bytes
```

This output instantly reveals that `Age` and `Salary` have missing values.

---

# 📌 Example 2 – Deep Memory Usage Check

```python
df.info(memory_usage="deep")
```

Setting `memory_usage="deep"` tells Pandas to accurately calculate the memory footprint of text (`object`) columns, providing a precise byte count rather than a rough estimate.

---

# 🏢 Real Industry Example

Suppose a Data Engineer pulls daily web traffic logs into a DataFrame.

Before running any models, they check:

```python
df.info()
```

If the `Timestamp` column shows a dtype of `object`, they immediately know they must convert it to `datetime64` before doing time-series forecasting. If a crucial column like `User_ID` is missing 40% of its values, they might halt the pipeline to fix the upstream data source.

---

# 🧠 Engineer Thinking

When looking at `info()`, ask yourself:

- Does the total number of rows match my expectations?
- Do the `dtypes` match the business reality? (Dates should be datetime, prices should be float).
- Are there columns with severe missing data (low non-null count) that should be dropped entirely?
- Is the memory usage dangerously close to my RAM limits?

---

# ⚡ Performance Notes

- `info()` calculates non-null counts, which can take a few seconds on datasets with millions of rows.
- If it is too slow, you can use `df.info(show_counts=False)` to skip the counting process.

---

# ✅ Best Practices

- Always run `info()` immediately after reading data.
- Write down the anomalies (like wrong dtypes or missing counts) to create a data cleaning checklist.
- Use `memory_usage="deep"` when working near memory limits.

---

# ❌ Common Mistakes

### Mistake 1

Ignoring `object` data types for numeric columns.

If a `Price` column is `object`, it likely contains dollar signs or commas. You must clean it before modeling.

---

### Mistake 2

Assuming the default memory usage is 100% accurate.

For string-heavy datasets, the default memory usage is an underestimation. Always use `"deep"` for accuracy.

---

# 💼 Interview Questions

### Q1. What does `info()` output?

It outputs the total rows, column names, non-null counts, data types, and estimated memory usage.

---

### Q2. How do you find missing values using `info()`?

By comparing the `RangeIndex` (total entries) with the `Non-Null Count` of each column. A lower non-null count indicates missing data.

---

### Q3. How do you get accurate memory usage for string columns?

By using `df.info(memory_usage="deep")`.

---

# 📌 Summary

- `info()` provides a technical metadata summary.
- It is the fastest way to check for missing values and data type mismatches.
- It helps you understand the memory constraints of your dataset.
- It is a foundational step in Exploratory Data Analysis (EDA).

---

# 🚀 Next Topic

The next topic is:

**05-describe().md**

You'll learn how to generate powerful statistical summaries for your data to identify distributions and outliers.
