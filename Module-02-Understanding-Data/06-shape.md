# 📐 shape in Pandas

> The `shape` attribute provides the dimensionality of your dataset. Knowing exactly how many rows and columns you are working with is crucial before applying heavy computations or merging tables.

---

# 📖 Table of Contents

1. Introduction
2. Learning Objectives
3. What is `shape`?
4. Why Do We Use `shape`?
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

- Understand the concept of dataset dimensionality.
- Retrieve the row and column count using `shape`.
- Extract row and column counts programmatically for data validation.

---

# 📘 What is `shape`?

`shape` is an **attribute** (not a function) of a Pandas DataFrame and Series.

It returns a tuple representing the dimensionality of the DataFrame in the format `(rows, columns)`.

---

# ❓ Why Do We Use `shape`?

Understanding the dimensions of your data helps you:

- **Estimate computation time**: Training a model on 10,000 rows takes seconds; on 10,000,000 rows it takes hours.
- **Validate operations**: If you drop missing values, you need to check `shape` before and after to see how much data was lost.
- **Verify joins**: When merging datasets, checking the `shape` ensures the merge didn't accidentally duplicate millions of rows.

---

# 📝 Syntax

```python
DataFrame.shape
```
*(Notice there are no parentheses because it is an attribute, not a method.)*

---

# ⚙️ Parameters

Since `shape` is an attribute, it takes **no parameters**.

---

# 💻 Example Dataset

```text
Employee_ID   Name      Age   Department   Salary
101           Ram       25    IT           50000
102           Ravi      28    HR           60000
103           John      30    Finance      70000
104           Priya     24    IT           55000
```

---

# 📌 Example 1 – Default Behavior

```python
import pandas as pd

df = pd.read_csv("employees.csv")

print(df.shape)
```

### Output

```text
(4, 5)
```

This means the dataset has **4 rows** and **5 columns**.

---

# 📌 Example 2 – Extracting specific dimensions

Since `shape` returns a tuple, you can access the row count and column count using indexing.

```python
num_rows = df.shape[0]
num_cols = df.shape[1]

print(f"Rows: {num_rows}, Columns: {num_cols}")
```

### Output

```text
Rows: 4, Columns: 5
```

---

# 🏢 Real Industry Example

An automated data pipeline runs every night to clean customer data.

The Data Engineer uses `shape` to write a validation test:

```python
original_shape = df.shape[0]

# Pipeline drops invalid emails
df_clean = clean_emails(df)

if df_clean.shape[0] < (original_shape * 0.9):
    raise ValueError("Too much data was lost during cleaning!")
```
This prevents a bug from silently deleting all the data.

---

# 🧠 Engineer Thinking

When using `shape`, ask yourself:

- Did the column count increase unexpectedly after a merge?
- How much data am I losing when I drop NaNs?
- Is my hardware capable of holding a dataset of this shape in memory?

---

# ⚡ Performance Notes

- `shape` is O(1). It executes instantly, regardless of whether your dataset has 10 rows or 10 billion rows, because Pandas already tracks the dimensions internally.

---

# ✅ Best Practices

- Print `shape` before and after filtering, dropping, or merging data.
- Use `shape[0]` when you need to dynamically size arrays or loops based on dataset size.

---

# ❌ Common Mistakes

### Mistake 1

Using parentheses like a function.

```python
# Error!
df.shape() 
```

`TypeError: 'tuple' object is not callable`

---

### Mistake 2

Confusing the tuple index.

Remember: `[0]` is rows, `[1]` is columns.

---

# 💼 Interview Questions

### Q1. Is `shape` a method or an attribute?

It is an attribute, which is why it does not use parentheses.

---

### Q2. What does `df.shape` return?

It returns a tuple in the format `(number_of_rows, number_of_columns)`.

---

### Q3. How do you get only the number of columns in a DataFrame?

By accessing the second element of the tuple: `df.shape[1]`.

---

# 📌 Summary

- `shape` provides the dimensions of the dataset.
- Returns a `(rows, columns)` tuple.
- It executes instantly and is heavily used in pipeline validation.

---

# 🚀 Next Topic

The next topic is:

**07-columns.md**

You'll learn how to access, inspect, and clean the column names of your DataFrame to ensure consistency across your project.
