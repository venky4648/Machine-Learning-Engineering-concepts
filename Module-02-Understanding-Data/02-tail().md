# 🔍 tail() in Pandas

> The `tail()` function is used to display the last few rows of a DataFrame. It helps verify the end of a dataset, detect incomplete records, and ensure that data has been loaded correctly from beginning to end.

---

# 📖 Table of Contents

1. Introduction
2. Learning Objectives
3. What is `tail()`?
4. Why Do We Use `tail()`?
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

- Understand the purpose of `tail()`.
- Display the last few rows of a dataset.
- Display a custom number of rows.
- Verify the end of the dataset.
- Detect missing or incomplete records at the bottom of a file.

---

# 📘 What is `tail()`?

The `tail()` function returns the **last _n_ rows** of a DataFrame.

By default, it returns the **last 5 rows**.

It is mainly used to inspect the end of the dataset without printing the entire DataFrame.

---

# ❓ Why Do We Use `tail()`?

Sometimes problems occur at the end of a dataset.

Examples:

- Incomplete records
- Extra blank rows
- Incorrect values
- Data appended incorrectly
- Import/export issues

Using `tail()` allows you to quickly inspect the last few rows and identify these issues.

---

# 📝 Syntax

```python
DataFrame.tail(n)
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

df.tail()
```

### Output

```text
   Employee_ID   Name   Age Department Salary
2          103   John    30   Finance  70000
3          104  Priya    24        IT  55000
4          105 Anjali    27     Sales  52000
5          106  Kiran    31        HR  65000
6          107  David    29   Finance  72000
```

By default, the last **5 rows** are displayed.

---

# 📌 Example 2 – Display Last 3 Rows

```python
df.tail(3)
```

### Output

```text
Employee_ID   Name    Age
105          Anjali   27
106          Kiran    31
107          David    29
```

---

# 📌 Example 3 – Display Last 10 Rows

```python
df.tail(10)
```

If the DataFrame contains fewer than 10 rows, Pandas returns all available rows.

---

# 🏢 Real Industry Example

Suppose your company exports daily transaction data.

The last few rows may contain:

- Recently added transactions
- Partial uploads
- Failed imports
- Corrupted records

Before processing, an engineer checks:

```python
df.tail()
```

This ensures the file ends correctly and does not contain unexpected data.

---

# 🧠 Engineer Thinking

When viewing the last rows, ask yourself:

- Are the records complete?
- Are there unexpected blank rows?
- Did the export finish successfully?
- Are IDs increasing correctly?
- Are dates in the expected range?
- Is the last record valid?

A Machine Learning Engineer doesn't just "look" at the data—they verify its integrity.

---

# ⚡ Performance Notes

- `tail()` is very efficient.
- It retrieves only the last few rows from the DataFrame.
- Suitable for datasets with millions of records.

---

# ✅ Best Practices

- Use `tail()` after `head()` when first exploring a dataset.
- Verify that the last records are complete.
- Check for accidental blank rows or corrupted data.
- Combine `tail()` with `shape` to understand dataset size.

---

# ❌ Common Mistakes

### Mistake 1

Assuming the end of the dataset is always correct.

Always verify it.

---

### Mistake 2

Using only `head()`.

Problems may exist only at the bottom of the dataset.

---

### Mistake 3

Using `tail()` instead of proper validation.

`tail()` is for inspection, not validation.

---

# 📊 head() vs tail()

| Feature | head() | tail() |
|----------|---------|---------|
| Displays | First rows | Last rows |
| Default Rows | 5 | 5 |
| Used For | Initial inspection | Final inspection |
| Common Purpose | Verify loading | Detect end-of-file issues |

---

# 💼 Interview Questions

### Q1. What does `tail()` return?

It returns the last **n** rows of a DataFrame.

---

### Q2. How many rows does `tail()` return by default?

**5 rows.**

---

### Q3. How do you display the last 8 rows?

```python
df.tail(8)
```

---

### Q4. Does `tail()` modify the original DataFrame?

No. It only returns a preview.

---

### Q5. Why should engineers inspect both `head()` and `tail()`?

Because issues may exist at either the beginning or the end of a dataset. Checking both provides a more complete initial inspection.

---

# 📌 Summary

- `tail()` displays the last few rows of a DataFrame.
- By default, it returns **5 rows**.
- It is useful for checking the end of a dataset.
- Engineers use it to identify incomplete or corrupted records.
- It is an important part of the initial data exploration process.

---

# 🚀 What's Next?

The next topic is:

**03-sample().md**

You'll learn how to randomly inspect records using `sample()`, which is especially useful for large datasets where the first or last rows may not represent the entire dataset.