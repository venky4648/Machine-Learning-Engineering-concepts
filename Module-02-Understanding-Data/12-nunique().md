# 🔢 nunique() in Pandas

> While `unique()` shows you *what* the distinct values are, `nunique()` tells you *how many* there are. This is a crucial concept known as **cardinality**, which heavily influences how you handle features in Machine Learning.

---

# 📖 Table of Contents

1. Introduction
2. Learning Objectives
3. What is `nunique()`?
4. Why Do We Use `nunique()`?
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

- Count the number of distinct values in a column or DataFrame.
- Understand the concept of feature cardinality.
- Control how missing values (`NaN`) are counted.

---

# 📘 What is `nunique()`?

The `nunique()` function stands for "number of unique". 

It counts the number of distinct elements along a specified axis. Unlike `unique()`, which only works on a single column (Series), `nunique()` can be applied to an entire DataFrame to get counts for every column at once.

---

# ❓ Why Do We Use `nunique()`?

In Machine Learning, **Cardinality** is the number of unique categories a feature has.

- **Low Cardinality** (e.g., `Gender` = 2, `Blood_Type` = 8): Perfect for One-Hot Encoding.
- **High Cardinality** (e.g., `Customer_ID` = 1,000,000, `Zip_Code` = 40,000): One-Hot Encoding this will crash your memory. You must use Target Encoding, embeddings, or drop the column.
- **Zero Variance** (e.g., `Is_Human` = 1): If a column only has 1 unique value, it contains zero predictive power and should be dropped.

`nunique()` instantly tells you the cardinality of your features.

---

# 📝 Syntax

```python
# On a specific column
Series.nunique(dropna=True)

# On the entire DataFrame
DataFrame.nunique(axis=0, dropna=True)
```

---

# ⚙️ Parameters

| Parameter | Description | Default |
|-----------|-------------|---------|
| `axis` | `0` for columns, `1` for rows | `0` |
| `dropna` | If `True`, missing values (`NaN`) are NOT counted. | `True` |

---

# 💻 Example Dataset

```text
ID    City       Status
1     NY         Active
2     LA         Inactive
3     NY         Active
4     NaN        Active
```

---

# 📌 Example 1 – Default Behavior

```python
import pandas as pd

df = pd.read_csv("data.csv")

# Get unique counts for all columns
print(df.nunique())
```

### Output

```text
ID        4
City      2
Status    2
dtype: int64
```
Notice that `City` returns 2 (NY, LA). It ignored the `NaN` value!

---

# 📌 Example 2 – Including Missing Values

To count `NaN` as a distinct category, change the `dropna` parameter.

```python
print(df.nunique(dropna=False))
```

### Output

```text
ID        4
City      3
Status    2
dtype: int64
```
Now `City` returns 3 (NY, LA, and NaN).

---

# 🏢 Real Industry Example

Before passing data into a Random Forest algorithm, an engineer runs:

```python
cardinality = df.nunique()
drop_cols = cardinality[cardinality == 1].index
df = df.drop(columns=drop_cols)
```

This brilliant snippet automatically drops any column that contains only 1 unique value, because zero-variance features offer absolutely no learning value to a model.

---

# 🧠 Engineer Thinking

When reviewing `nunique()`, ask yourself:

- Does the `nunique()` of `User_ID` equal the total rows in the dataset? If not, there are duplicate records.
- Does a Boolean column have 3 unique values instead of 2? (Usually means True, False, and NaN).
- Which columns have high cardinality and need special encoding strategies?

---

# ⚡ Performance Notes

- Running `nunique()` on a DataFrame with many string columns can take some time, as it has to hash and count every string.

---

# ✅ Best Practices

- Use `nunique()` to identify and drop constant features (cardinality == 1).
- Use it as a quick check for primary keys. If `df['ID'].nunique() == df.shape[0]`, the IDs are perfectly unique.

---

# ❌ Common Mistakes

### Mistake 1

Assuming `nunique()` counts `NaN` by default.

Unlike `unique()`, `nunique()` **drops** `NaN` values by default. You must pass `dropna=False` if you want missing values counted.

---

# 💼 Interview Questions

### Q1. What is the difference between `unique()` and `nunique()`?

`unique()` returns an array of the actual distinct values, and only works on a Series. `nunique()` returns the integer count of those values, and works on both Series and DataFrames.

---

### Q2. Does `nunique()` count missing values?

Not by default. You must specify `dropna=False` for it to include `NaN` in the count.

---

### Q3. How do you find columns that provide no predictive value using `nunique()`?

By finding columns where `df.nunique() == 1`. These constant columns provide no variance for a model to learn from.

---

# 📌 Summary

- `nunique()` returns the count of distinct values.
- It is the primary tool for evaluating feature cardinality.
- By default, it ignores `NaN` values.
- It can be applied to both Series and whole DataFrames.

---

# 🚀 Next Topic

The next topic is:

**13-value_counts().md**

You'll learn how to calculate the frequency distribution of categorical data, which is essential for identifying class imbalance in Machine Learning targets.
