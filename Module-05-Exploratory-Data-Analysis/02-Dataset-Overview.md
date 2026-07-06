# 🗺️ Dataset Overview

> Before diving into deep statistical math, you need a high-level map of your data. The Dataset Overview phase establishes the basic shape, size, and layout of your DataFrame.

---

# 📖 Table of Contents

1. Introduction
2. Learning Objectives
3. What is a Dataset Overview?
4. Why Do We Use It?
5. Syntax (`head`, `tail`, `sample`, `shape`, `columns`, `index`)
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

- Use `head()`, `tail()`, and `sample()` to preview records.
- Retrieve dimensions using `shape`.
- Extract structural metadata using `columns` and `index`.

---

# 📘 What is a Dataset Overview?

A Dataset Overview utilizes basic Pandas commands to inspect the physical structure of the loaded data. It verifies that the CSV/SQL data translated into a Pandas DataFrame correctly.

---

# ❓ Why Do We Use It?

You cannot analyze what you cannot see. If your dataset has 1 million rows and 500 columns, you need tools to grab quick, memory-efficient snapshots of the top, bottom, and random cross-sections of the data to ensure the import was successful.

---

# 📝 Syntax

```python
df.head(n)       # First n rows
df.tail(n)       # Last n rows
df.sample(n)     # Random n rows
df.shape         # (Rows, Columns) tuple
df.columns       # List of column names
df.index         # Row labels/indices
```

---

# ⚙️ Parameters

| Function | Parameter | Description | Default |
|----------|-----------|-------------|---------|
| `head/tail`| `n` | Number of rows to display | `5` |
| `sample` | `n` | Number of random rows to select | `1` |
| `sample` | `random_state`| Seed for reproducibility | `None` |

---

# 💻 Example Dataset

Imagine a large `transactions.csv` containing user purchase data.

---

# 📌 Example 1 – Peeking at the Data

```python
import pandas as pd

df = pd.read_csv('transactions.csv')

# Verify the header parsed correctly
print(df.head())

# Check for garbage totals at the bottom of the file
print(df.tail())

# Take an unbiased random look
print(df.sample(5, random_state=42))
```

---

# 📌 Example 2 – Structural Verification

```python
# How big is this data?
print(df.shape) 
# Output: (1000000, 15)

# What are the exact column names?
print(df.columns)
# Output: Index(['txn_id', 'amount', 'date', ...])
```

---

# 🏢 Real Industry Example

A Data Engineer sets up an automated Airflow job. To ensure the daily data pull is valid, they write a simple script:

```python
if df.shape[0] < 1000:
    raise ValueError("Dataset is too small! Data pull likely failed.")
```
Using `shape` allows them to instantly validate the size of the dataset before passing it downstream to the Data Scientists.

---

# 🧠 Engineer Thinking

When performing an overview, ask yourself:

- Does `shape` match the business expectation? (e.g., "I requested 10 years of daily data. 10 * 365 = 3650 rows. Does `shape[0]` equal ~3650?")
- Are there spaces hidden in `df.columns`?
- Does `tail()` reveal Excel-style summary rows ("Total:") that will break my models?

---

# ⚡ Performance Notes

- All of these operations (`head`, `shape`, `columns`) execute in `O(1)` time. They are instantaneous, making them the perfect first step for any size dataset.

---

# ✅ Best Practices

- Always combine `head()` and `tail()`. `head()` often looks perfectly clean while the bottom of the file is a disaster.
- Use `sample()` to avoid the bias of chronologically sorted data.

---

# ❌ Common Mistakes

### Mistake 1
Printing the entire DataFrame (`print(df)`). This can cause Jupyter Notebooks to freeze or crash if the dataset is massive. Always use `head()` or `sample()`.

---

# 💼 Interview Questions

### Q1. What is the difference between `head()` and `sample()`?
`head()` returns the first sequentially ordered rows, while `sample()` returns a random, unbiased subset of rows from anywhere in the DataFrame.

### Q2. Is `shape` a method or an attribute?
It is an attribute, which is why it is called without parentheses.

---

# 📌 Summary

- `head()`, `tail()`, and `sample()` provide visual verification of data records.
- `shape`, `columns`, and `index` provide structural metadata.
- These commands are the absolute mandatory first step of EDA.

---

# 🚀 Next Topic

The next topic is:

**03-Statistical-Summary.md**

You'll move from structural overviews into mathematical analysis using functions like `describe()`, `mean()`, and `std()`.
