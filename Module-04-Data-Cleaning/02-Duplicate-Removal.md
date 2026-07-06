# 👯 Duplicate Removal in Pandas

> Duplicates occur when the exact same record exists multiple times in a dataset. If left unchecked, duplicates can artificially boost a model's confidence and skew summary statistics.

---

# 📖 Table of Contents

1. Introduction
2. Learning Objectives
3. What are Duplicates?
4. Why Do We Care About Duplicates?
5. Syntax & Detection
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

- Detect duplicate rows across an entire DataFrame.
- Detect duplicates based on specific primary key columns.
- Remove duplicates safely while choosing which record to keep.

---

# 📘 What are Duplicates?

Duplicates are identical rows (or partially identical rows, depending on your logic) present in a DataFrame. 

They usually result from:
- A user clicking "Submit" twice on a web form.
- Data being appended to a database multiple times by accident.
- Joins (SQL or Pandas merges) that cause a one-to-many explosion.

---

# ❓ Why Do We Care About Duplicates?

1. **Statistical Skew**: If a rare event (like a specific fraudulent transaction) is accidentally duplicated 1,000 times, your model will think this type of fraud is incredibly common.
2. **Train/Test Contamination**: If the same record exists in both your training set and your test set, your model isn't predicting; it is memorizing.

---

# 📝 Syntax & Detection

```python
# Detect duplicates (returns boolean mask)
DataFrame.duplicated()

# Count duplicates
DataFrame.duplicated().sum()

# Remove duplicates
DataFrame.drop_duplicates()
```

---

# ⚙️ Parameters

For `drop_duplicates()`:

| Parameter | Description | Default |
|-----------|-------------|---------|
| `subset` | Column(s) to consider when identifying duplicates. | `None` (uses all columns) |
| `keep` | Determines which duplicate to keep: `'first'`, `'last'`, or `False` (drop all). | `'first'` |
| `inplace`| Whether to drop duplicates in place or return a copy. | `False` |

---

# 💻 Example Dataset

```text
User_ID   Name      City
101       Ram       NY
102       Ravi      LA
101       Ram       NY    <-- Exact Duplicate
103       John      CHI
103       John      MIA   <-- Partial Duplicate (Same User_ID, different City)
```

---

# 📌 Example 1 – Finding and Dropping Exact Duplicates

By default, Pandas checks if *every single column* is identical.

```python
import pandas as pd

df = pd.read_csv("users.csv")

# See how many exact duplicates exist
print("Duplicates:", df.duplicated().sum())

# Drop exact duplicates
df_clean = df.drop_duplicates()
```

### Output

Row 3 (Ram, NY) is dropped. Row 1 is kept because `keep='first'` is the default.

---

# 📌 Example 2 – Dropping Partial Duplicates (Based on Subset)

Sometimes a user updates their profile, resulting in two rows with the same `User_ID` but different `City` values. We only want one row per `User_ID`.

```python
# Keep the most recent entry (the last one)
df_unique_users = df.drop_duplicates(subset=['User_ID'], keep='last')
```

### Output

Row 4 (John, CHI) is dropped. Row 5 (John, MIA) is kept because we specified `keep='last'`.

---

# 🏢 Real Industry Example

An E-Commerce Data Engineer is processing a daily log of website clicks. A bug in the front-end caused the website to send two identical clicks every time a user pressed the "Buy" button within the same second.

The engineer uses `df.drop_duplicates(subset=['User_ID', 'Timestamp', 'Action'])` to remove the second click. If they had skipped this step, the company's "Conversion Rate" metrics would be falsely doubled!

---

# 🧠 Engineer Thinking

When looking at duplicates, ask yourself:

- Are these *true* exact duplicates, or is there a tiny timestamp difference that makes them unique?
- If I drop duplicates based on a `User_ID`, which row is the most accurate? The first one, or the last one?
- Should I sort the DataFrame by `Date` before dropping duplicates to ensure `keep='last'` actually keeps the most recent data?

---

# ⚡ Performance Notes

- `drop_duplicates()` is highly optimized, but running it on a massive DataFrame with 100+ columns is memory intensive. It is much faster to use the `subset` parameter to check duplicates on just 2 or 3 primary key columns.

---

# ✅ Best Practices

- If applying `subset`, **sort your data first** (e.g., by Date descending) so you have absolute control over what `keep='first'` actually means.
- Always check the `shape` before and after dropping to document how many rows were removed.

---

# ❌ Common Mistakes

### Mistake 1

Using `keep=False`.

```python
df.drop_duplicates(keep=False)
```
This drops ALL instances of the duplicate. If Ram appeared twice, BOTH rows are deleted, and Ram is completely wiped from your dataset. Only use this if duplicates indicate completely corrupted, untrustworthy data.

---

# 💼 Interview Questions

### Q1. How do you remove duplicates based on a specific column rather than the whole row?
By using the `subset` parameter: `df.drop_duplicates(subset=['Column_Name'])`.

---

### Q2. How do you ensure you keep the most recently updated record when dropping duplicates?
First, sort the DataFrame by the Date/Time column. Then use `drop_duplicates(subset=['ID'], keep='last')` (or `'first'`, depending on your sort order).

---

# 📌 Summary

- Exact duplicates skew machine learning models and analytics.
- Use `duplicated().sum()` to check for the presence of duplicates.
- Use `drop_duplicates()` to remove them.
- Utilize the `subset` and `keep` parameters for advanced logic (like keeping the most recent record of a user).

---

# 🚀 Next Topic

The next topic is:

**03-Data-Type-Conversion.md**

You'll learn how to forcefully correct columns that have loaded with the wrong data type (like converting text prices into usable floats).
