# 🔚 Using `tail()` in Pandas

> While `head()` checks the top of your dataset, `tail()` checks the bottom. Real-world datasets, especially those exported from Excel or enterprise reporting tools, often hide garbage data, totals, or metadata at the very end.

---

# 📖 Table of Contents

1. What is `tail()`?
2. Why Use `tail()`?
3. Basic Usage
4. Customizing the Number of Rows
5. Industry Best Practices
6. Common Errors
7. Interview Questions
8. Summary

---

# 🎯 Learning Objectives

After completing this topic, you will be able to:
- Use `df.tail()` to preview the end of a dataset.
- Identify common data issues that occur at the bottom of files.

---

# 📘 What is `tail()`?

The `tail()` method in Pandas returns the **last n rows** of a DataFrame or Series.

By default, it returns the **last 5 rows**.

---

# 🏢 Why Do Companies Use `tail()`?

In industry, `tail()` is highly useful for:
- **Spotting Footer Garbage**: Excel exports often have rows at the bottom like `"Report generated on 2023-10-01"` or `"Total: $1,000,000"`.
- **Chronological Data**: For time-series data appended daily, `tail()` shows you the most recent records.
- **Checking Data Size**: Looking at the index of the last row gives you a quick idea of how many rows the dataset has (if the index is a standard RangeIndex).

---

# 📂 Basic Usage

```python
import pandas as pd

df = pd.read_csv("sales_data.csv")

# Preview the last 5 rows
print(df.tail())
```

**Output:**
```text
      Date      Item  Quantity  Revenue
995  2023-12-27   Mouse         2       40
996  2023-12-28  Laptop         1     1200
997  2023-12-29 Monitor         1      300
998         NaN   Total       950    45000   <-- (Wait, this is an Excel summary row!)
999  Report ends here    NaN       NaN      NaN   <-- (Garbage text)
```
*Notice how `tail()` instantly revealed data quality issues that `head()` would have completely missed!*

---

# ⚙️ Customizing the Number of Rows

Like `head()`, pass an integer `n` to view a specific number of rows from the bottom.

```python
# View the last 3 rows
df.tail(3)
```

---

# ⚡ Industry Best Practices

✅ **Always check `tail()` for Excel/CSV exports**: Business reports almost always have summary totals at the bottom. You must remove these before training Machine Learning models, otherwise your model will think "Total" is a category!
✅ **Use `tail()` for Time-Series validation**: If data is sorted chronologically, `tail()` confirms if your data pull includes yesterday's data as expected.

---

# ❌ Common Mistakes

### Mistake 1: Forgetting that `tail()` exists
Many beginners only run `head()`, see clean data, and assume the whole dataset is clean. They then get a `ValueError` during modeling because row 9,999 contained text instead of a number.

---

# 💼 Interview Questions

### Q1. What does `df.tail()` return?
It returns the last 5 rows of a DataFrame by default.

### Q2. Why is running `tail()` just as important as running `head()`?
Because real-world datasets often contain summary statistics, metadata, or corrupted lines at the very end of the file.

---

# 🧠 Engineer Thinking

When reviewing `tail()`, ask yourself:
- Is the last row actual data, or is it a summary/aggregate row?
- Does the data suddenly change formatting near the end?
- Is the index contiguous, or are there missing index numbers?

---

# 📌 Summary

- `tail()` shows the bottom rows of your data.
- Default is 5 rows.
- Crucial for identifying trailing metadata and summary rows.

---

# 🚀 What's Next?

The next topic is:

**[03-sample().md](03-sample().md)**

You will learn how to pull random rows from your dataset, which prevents bias when evaluating the structure of your data.
