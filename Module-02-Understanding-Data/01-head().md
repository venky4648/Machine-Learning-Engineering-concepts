# 👀 Using `head()` in Pandas

> `head()` is usually the very first function a Machine Learning Engineer runs after loading a dataset. It gives you a quick snapshot of the data structure without crashing your memory.

---

# 📖 Table of Contents

1. What is `head()`?
2. Why Use `head()`?
3. Basic Usage
4. Customizing the Number of Rows
5. Industry Best Practices
6. Common Errors
7. Interview Questions
8. Summary

---

# 🎯 Learning Objectives

After completing this topic, you will be able to:
- Use `df.head()` to preview data.
- Understand the default behavior of the function.
- Change the number of rows displayed.

---

# 📘 What is `head()`?

The `head()` method in Pandas returns the **first n rows** of a DataFrame or Series.

By default, it returns the **first 5 rows**.

---

# 🏢 Why Do Companies Use `head()`?

When working with massive datasets (e.g., millions of rows), printing the entire DataFrame will clutter your screen and slow down your environment (like Jupyter Notebooks). `head()` allows you to quickly verify:
- Are the column names parsed correctly?
- Are the data types what I expect?
- Did the file read successfully without shifting columns?

---

# 📂 Basic Usage

```python
import pandas as pd

# Load data
df = pd.read_csv("employees.csv")

# Preview the first 5 rows
print(df.head())
```

**Output:**
```text
   Emp_ID   Name  Age Department  Salary
0     101    Ram   25         IT   50000
1     102   John   30    Finance   70000
2     103  Priya   28         HR   60000
3     104   Alex   35         IT   80000
4     105   Sara   29  Marketing   55000
```

---

# ⚙️ Customizing the Number of Rows

You can pass an integer `n` to see a specific number of rows.

```python
# View only the first 2 rows
df.head(2)

# View the first 10 rows
df.head(10)
```

---

# ⚡ Industry Best Practices

✅ **Always run `head()` after reading data**: Make it a habit. It instantly confirms if your `read_csv()` (or other read function) parameters worked correctly (e.g., if you needed to use `skiprows` or `header=None`).
✅ **Combine with transposing for wide datasets**: If you have 100 columns, `df.head().T` makes it easier to read all column names and their first 5 values vertically.

---

# ❌ Common Mistakes

### Mistake 1: Relying *only* on `head()`
Just because the first 5 rows look clean doesn't mean row 1,000,000 is clean. `head()` is not a substitute for proper data validation or checking `tail()` and `sample()`.

---

# 💼 Interview Questions

### Q1. What does `df.head()` return by default?
It returns the first 5 rows of the DataFrame.

### Q2. How can you view the first 15 rows of a dataset?
By calling `df.head(15)`.

---

# 🧠 Engineer Thinking

When looking at the output of `head()`, ask yourself:
- Does the data look like what the business team promised?
- Are there obvious `NaN` values right at the top?
- Do the indexes start at 0, or is there a weird offset?

---

# 📌 Summary

- `head()` shows the top rows of your data.
- Default is 5 rows.
- Use `df.head(n)` to specify the row count.

---

# 🚀 What's Next?

The next topic is:

**[02-tail().md](02-tail().md)**

You will learn how to check the *bottom* of your dataset, which is crucial for finding incomplete appends, summary rows, or footer text hidden at the end of files.
