# 🎲 sample() in Pandas

> The `sample()` function is used to randomly select rows from a DataFrame. Unlike `head()` and `tail()`, which always show the beginning or end of a dataset, `sample()` gives a random view of the data. This helps engineers inspect different parts of the dataset without introducing positional bias.

---

# 📖 Table of Contents

1. Introduction
2. Learning Objectives
3. What is `sample()`?
4. Why Do We Use `sample()`?
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

- Understand the purpose of `sample()`.
- Randomly inspect records from a dataset.
- Select a custom number of random rows.
- Create reproducible random samples.
- Understand when to use sampling in Machine Learning workflows.

---

# 📘 What is `sample()`?

The `sample()` function returns **random rows** from a DataFrame.

Unlike:

- `head()` → First rows
- `tail()` → Last rows

`sample()` selects rows randomly from anywhere in the dataset.

This helps reduce bias when inspecting data.

---

# ❓ Why Do We Use `sample()`?

Suppose a dataset contains **5 million rows**.

If you only inspect:

```python
df.head()
```

you only see the beginning.

If you inspect:

```python
df.tail()
```

you only see the end.

But important issues may exist in the middle.

Using:

```python
df.sample()
```

provides a random snapshot of the dataset.

---

# 📝 Syntax

```python
DataFrame.sample(
    n=None,
    frac=None,
    replace=False,
    random_state=None
)
```

---

# ⚙️ Parameters

| Parameter | Description | Default |
|-----------|-------------|---------|
| `n` | Number of random rows | 1 |
| `frac` | Fraction of rows to return | None |
| `replace` | Sample with replacement | False |
| `random_state` | Seed for reproducibility | None |

---

# 💻 Example Dataset

```text
Employee_ID   Name     Age   Department   Salary
101           Ram      25    IT           50000
102           Ravi     28    HR           60000
103           John     30    Finance      70000
104           Priya    24    IT           55000
105           Anjali   27    Sales        52000
106           Kiran    31    HR           65000
107           David    29    Finance      72000
108           Rahul    26    Marketing    51000
109           Sneha    32    HR           75000
110           Neha     23    Sales        48000
```

---

# 📌 Example 1 – Default Behavior

```python
import pandas as pd

df = pd.read_csv("employees.csv")

df.sample()
```

### Possible Output

```text
Employee_ID   Name   Age Department Salary
106          Kiran   31      HR     65000
```

By default, `sample()` returns **1 random row**.

---

# 📌 Example 2 – Select 5 Random Rows

```python
df.sample(n=5)
```

### Possible Output

```text
102 Ravi
110 Neha
105 Anjali
103 John
108 Rahul
```

The output changes each time you run the code.

---

# 📌 Example 3 – Select 30% of the Dataset

```python
df.sample(frac=0.3)
```

If the dataset has **100 rows**, this returns approximately **30 random rows**.

---

# 📌 Example 4 – Reproducible Sampling

```python
df.sample(
    n=5,
    random_state=42
)
```

Every time you run this code, the **same 5 rows** are returned.

This is useful for:

- Machine Learning experiments
- Testing
- Debugging
- Documentation

---

# 📌 Example 5 – Sampling With Replacement

```python
df.sample(
    n=10,
    replace=True
)
```

Since `replace=True`, the same row can appear multiple times in the sample.

This is commonly used in techniques such as **bootstrapping**.

---

# 🏢 Real Industry Example

A company has **20 million customer records**.

Inspecting every record manually is impossible.

Instead, an engineer randomly samples a few hundred rows:

```python
df.sample(n=500)
```

This helps identify:

- Incorrect values
- Missing information
- Formatting issues
- Unexpected categories

without reviewing the entire dataset.

---

# 🧠 Engineer Thinking

When using `sample()`, ask yourself:

- Does the random sample represent the dataset?
- Are there unexpected values?
- Do different departments appear?
- Are missing values spread throughout the data?
- Are categories balanced?
- Should I fix the random seed (`random_state`) for reproducibility?

Random inspection often reveals problems that `head()` and `tail()` cannot.

---

# ⚡ Performance Notes

- `sample()` is efficient for most datasets.
- For very large datasets, sampling is much faster than inspecting every row.
- Use `random_state` whenever reproducibility is required.

---

# ✅ Best Practices

- Use `sample()` after `head()` and `tail()`.
- Set `random_state` for repeatable results.
- Use `frac` when you need a percentage of the data.
- Use `replace=True` only when duplicate sampling is intended.

---

# ❌ Common Mistakes

### Mistake 1

Assuming one random sample represents the entire dataset.

Take multiple samples if needed.

---

### Mistake 2

Forgetting `random_state`.

Without it, each execution produces different results.

---

### Mistake 3

Using both `n` and `frac` together.

Choose **either** `n` **or** `frac`, not both.

---

### Mistake 4

Using `replace=True` unintentionally.

This can result in duplicate rows appearing in the sample.

---

# 📊 head() vs tail() vs sample()

| Function | Returns | Common Use |
|----------|---------|------------|
| `head()` | First rows | Verify beginning of dataset |
| `tail()` | Last rows | Verify end of dataset |
| `sample()` | Random rows | Random inspection of dataset |

---

# 💼 Interview Questions

### Q1. What does `sample()` do?

It returns randomly selected rows from a DataFrame.

---

### Q2. How many rows does `sample()` return by default?

**1 row.**

---

### Q3. What is the purpose of `random_state`?

It ensures the same random sample is generated every time the code runs, making experiments reproducible.

---

### Q4. What is the difference between `n` and `frac`?

- `n` specifies the exact number of rows.
- `frac` specifies the fraction (percentage) of the dataset.

---

### Q5. When should `replace=True` be used?

When sampling with replacement is required, such as in bootstrapping or certain statistical techniques.

---

# 📌 Summary

- `sample()` returns random rows from a DataFrame.
- It helps inspect different parts of a dataset.
- Use `n` for a fixed number of rows.
- Use `frac` for a percentage of rows.
- Use `random_state` for reproducible results.
- It complements `head()` and `tail()` during data exploration.

---

# 🚀 What's Next?

The next topic is:

**04-info().md**

You'll learn how to inspect the overall structure of a DataFrame, including column names, data types, non-null counts, and memory usage. This is one of the most important functions in the data understanding phase.