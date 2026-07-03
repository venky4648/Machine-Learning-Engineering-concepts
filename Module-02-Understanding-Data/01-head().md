# 👀 head() in Pandas

> The `head()` function is one of the first functions every Data Analyst, Data Scientist, and Machine Learning Engineer uses after loading a dataset. It allows you to quickly preview the first few rows and verify that the data has been loaded correctly.

---

# 📖 Table of Contents

1. Introduction
2. Learning Objectives
3. What is `head()`?
4. Why Do We Use `head()`?
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

- Understand the purpose of `head()`.
- Preview the first few rows of a dataset.
- Display a custom number of rows.
- Verify whether data has loaded correctly.
- Use `head()` as part of your data exploration workflow.

---

# 📘 What is `head()`?

The `head()` function returns the **first _n_ rows** of a DataFrame.

By default, it returns the **first 5 rows**.

It is mainly used to **inspect the beginning of the dataset** without printing the entire DataFrame.

---

# ❓ Why Do We Use `head()`?

Imagine a dataset with **10 million rows**.

Printing the whole dataset is:

- Slow
- Difficult to read
- Memory intensive

Instead, `head()` lets you quickly inspect the beginning of the dataset to confirm that it has been loaded correctly.

---

# 📝 Syntax

```python
DataFrame.head(n)
```

---

# ⚙️ Parameters

| Parameter | Description | Default |
|-----------|-------------|---------|
| `n` | Number of rows to display | `5` |

---

# 💻 Example Dataset

```text
Employee_ID   Name      Age   Department   Salary
101           Ram       25    IT           50000
102           Ravi      28    HR           60000
103           John      30    Finance      70000
104           Priya     24    IT           55000
105           Anjali    27    Sales        52000
106           Kiran     31    HR           65000
107           David     29    Finance      72000
```

---

# 📌 Example 1 – Default Behavior

```python
import pandas as pd

df = pd.read_csv("employees.csv")

df.head()
```

### Output

```text
   Employee_ID   Name   Age Department Salary
0          101    Ram    25        IT   50000
1          102   Ravi    28        HR   60000
2          103   John    30   Finance  70000
3          104  Priya    24        IT   55000
4          105 Anjali    27     Sales  52000
```

Only the **first 5 rows** are displayed.

---

# 📌 Example 2 – Display First 3 Rows

```python
df.head(3)
```

### Output

```text
Employee_ID   Name   Age
101           Ram    25
102           Ravi   28
103           John   30
```

---

# 📌 Example 3 – Display First 10 Rows

```python
df.head(10)
```

If the dataset contains fewer than 10 rows, Pandas returns all available rows.

---

# 🏢 Real Industry Example

Suppose your company provides a file named:

```text
employee_data.csv
```

Before cleaning or validating the data, the first thing an engineer does is:

```python
df = pd.read_csv("employee_data.csv")

df.head()
```

This quick check helps answer questions like:

- Did the file load correctly?
- Are the column names correct?
- Does the data look reasonable?
- Are there any obvious formatting issues?

---

# 🧠 Engineer Thinking

When using `head()`, don't just look at the rows.

Ask yourself:

- Are the column names correct?
- Do the values make sense?
- Are there unexpected missing values?
- Is the delimiter correct?
- Did the file load properly?
- Are the date formats correct?
- Does anything look suspicious?

`head()` is not just for viewing data—it's your **first quality check**.

---

# ⚡ Performance Notes

- `head()` is extremely fast because it only reads the first few rows from the DataFrame already in memory.
- It does **not** scan the entire dataset.
- Suitable even for very large datasets.

---

# ✅ Best Practices

- Always call `head()` immediately after reading a dataset.
- Combine it with `info()` to understand structure.
- Use it before validation and cleaning.
- Use a small value (5–10 rows) for quick inspection.

---

# ❌ Common Mistakes

### Mistake 1

Printing the entire DataFrame.

```python
print(df)
```

For large datasets, this is unnecessary and hard to read.

---

### Mistake 2

Assuming the data is correct just because `head()` looks fine.

Remember: `head()` only shows the **beginning** of the dataset.

Always inspect the dataset further using functions like `tail()`, `info()`, and validation checks.

---

### Mistake 3

Using `head()` as a replacement for validation.

`head()` helps you **preview** the data—it does not detect duplicates, missing values, or invalid data types.

---

# 💼 Interview Questions

### Q1. What does `head()` do?

It returns the first **n** rows of a DataFrame.

---

### Q2. How many rows does `head()` return by default?

**5 rows.**

---

### Q3. How do you display the first 10 rows?

```python
df.head(10)
```

---

### Q4. Does `head()` modify the original DataFrame?

No. It only returns a preview.

---

### Q5. Is `head()` suitable for large datasets?

Yes. It is efficient because it displays only a small number of rows.

---

# 📌 Summary

- `head()` is used to preview the beginning of a dataset.
- By default, it returns the first **5 rows**.
- You can specify a custom number of rows using the `n` parameter.
- It helps verify that data has been loaded correctly.
- It is the first step in understanding a dataset before validation or cleaning.

---

# 🚀 What's Next?

The next topic is:

**02-tail().md**

You'll learn how to inspect the **last few rows** of a dataset and why engineers use `tail()` to detect issues that may appear at the end of data files.