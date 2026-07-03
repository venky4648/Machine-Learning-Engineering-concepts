# 🧬 dtypes in Pandas

> Machine Learning models only understand numbers. If a numeric feature is accidentally stored as text, model training will crash. The `dtypes` attribute is your primary tool for preventing these fatal formatting bugs.

---

# 📖 Table of Contents

1. Introduction
2. Learning Objectives
3. What is `dtypes`?
4. Why Do We Use `dtypes`?
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

- Identify the exact data type of every column in a dataset.
- Understand the mapping between Python types and Pandas types.
- Select columns dynamically based on their data type.

---

# 📘 What is `dtypes`?

`dtypes` is an **attribute** (not a function) that returns a Series containing the data type of each column in the DataFrame.

### Common Pandas Data Types:
- `int64`: Integer numbers (e.g., 25, 100)
- `float64`: Decimal numbers (e.g., 25.5, 3.14)
- `object`: Text/Strings or mixed types (e.g., "Hello", "$500")
- `datetime64`: Dates and Times (e.g., 2023-10-01)
- `bool`: True/False values
- `category`: Categorical data with fixed, limited values

---

# ❓ Why Do We Use `dtypes`?

Data types dictate what operations you can perform. 

- You cannot calculate the mean of an `object` column.
- You cannot pass `object` columns into Scikit-Learn models without encoding them first.
- If a CSV file contains a single text value (like `"N/A"`) in a column of a million integers, Pandas forces the entire column to become an `object`. Checking `dtypes` instantly alerts you to this contamination.

---

# 📝 Syntax

```python
# View data types
DataFrame.dtypes

# Filter by data types
DataFrame.select_dtypes(include=None, exclude=None)
```

---

# ⚙️ Parameters

Since `dtypes` is an attribute, it takes no parameters.

For the `select_dtypes()` method:

| Parameter | Description | Default |
|-----------|-------------|---------|
| `include` | A list of data types to include | `None` |
| `exclude` | A list of data types to omit | `None` |

---

# 💻 Example Dataset

```text
Emp_ID   Name     Age   Salary    Is_Active
101      Ram      25    50000.5   True
102      Ravi     28    60000.0   False
```

---

# 📌 Example 1 – Default Behavior

```python
import pandas as pd

df = pd.read_csv("employees.csv")

print(df.dtypes)
```

### Output

```text
Emp_ID         int64
Name          object
Age            int64
Salary       float64
Is_Active       bool
dtype: object
```

---

# 📌 Example 2 – Filtering by Data Type

In ML pipelines, you often need to separate numeric columns (to scale them) from categorical columns (to encode them).

```python
# Select only numeric columns
numeric_df = df.select_dtypes(include=['int64', 'float64'])

# Select only categorical/text columns
text_df = df.select_dtypes(include=['object'])
```

---

# 🏢 Real Industry Example

A Machine Learning Engineer is building a pricing model. They load the dataset and check `dtypes`. 

They notice that `Price` is listed as an `object`. Upon inspection, they realize the web scraper captured prices as `"$1,500.00"`. Because of the `$` and `,`, Pandas treated it as text.

They immediately write a script to strip those characters and convert the column to `float64` before proceeding to EDA.

---

# 🧠 Engineer Thinking

When looking at `dtypes`, ask yourself:

- Does the `dtype` align with the real-world meaning of the feature? (Dates should be datetime, prices should be float).
- Are there "Hidden String" bugs? (A numeric column parsed as `object`).
- Can I optimize memory? (If an `int64` column only contains values from 0 to 10, changing it to `int8` saves massive amounts of memory).

---

# ⚡ Performance Notes

- Data type optimization is a massive part of Big Data engineering. Converting repetitive `object` text strings into `category` types can reduce memory usage by over 80%.

---

# ✅ Best Practices

- Validate `dtypes` early in your workflow.
- Use `select_dtypes` to build robust preprocessing pipelines that dynamically find numeric features, rather than hardcoding column names.

---

# ❌ Common Mistakes

### Mistake 1

Assuming `object` only means strings.

If a column has a mix of integers, floats, and strings, Pandas falls back to `object` to accommodate all of them.

---

### Mistake 2

Ignoring date columns.

Pandas often reads dates as `object` (strings). You must explicitly convert them using `pd.to_datetime()` to use time-series features.

---

# 💼 Interview Questions

### Q1. What does it mean if a numeric column's dtype is `object`?

It means the column contains mixed data types or was parsed entirely as strings due to dirty data (like commas, currency symbols, or "N/A" strings).

---

### Q2. How do you programmatically separate numeric features from categorical features?

By using `df.select_dtypes(include=['number'])` for numerical data, and `df.select_dtypes(include=['object', 'category'])` for categorical data.

---

### Q3. Why is the `category` dtype important?

It drastically reduces memory usage and speeds up computations when a text column has a limited number of unique values (low cardinality).

---

# 📌 Summary

- `dtypes` shows the data type of each column.
- Machine Learning models require numerical formats (`int64` or `float64`).
- `object` types are usually text and require cleaning or encoding.
- Use `select_dtypes` for intelligent feature separation in pipelines.

---

# 🚀 Next Topic

The next topic is:

**10-memory_usage().md**

You'll learn how to measure the RAM footprint of your DataFrame, an essential skill for processing large datasets without crashing your computer.
