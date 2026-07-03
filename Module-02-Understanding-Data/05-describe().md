# 📊 describe() in Pandas

> The `describe()` function generates descriptive statistics. It is your first step into statistical Exploratory Data Analysis (EDA), allowing you to quickly spot data distributions, central tendencies, and potential outliers.

---

# 📖 Table of Contents

1. Introduction
2. Learning Objectives
3. What is `describe()`?
4. Why Do We Use `describe()`?
5. Syntax
6. Parameters
7. Example Dataset
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

- Understand the purpose of `describe()`.
- Generate summary statistics for numeric data.
- Generate summary statistics for categorical data.
- Interpret percentiles to identify skewness and outliers.

---

# 📘 What is `describe()`?

The `describe()` function calculates summary statistics for the columns of a DataFrame.

By default, it only computes statistics for **numeric** (integer and float) columns.

It calculates:

- `count`: Number of non-null values
- `mean`: Average value
- `std`: Standard deviation
- `min`: Minimum value
- `25%`: 25th percentile (1st Quartile)
- `50%`: 50th percentile (Median)
- `75%`: 75th percentile (3rd Quartile)
- `max`: Maximum value

---

# ❓ Why Do We Use `describe()`?

While `info()` tells you the structure, `describe()` tells you the **behavior** of the data.

Using `describe()` helps you identify:

- **Outliers**: If the 75th percentile is 100 but the max is 10,000, you have extreme outliers.
- **Errors**: If the minimum Age is -5, you have bad data.
- **Skewness**: If the mean and median (50%) are vastly different, your data is skewed.

---

# 📝 Syntax

```python
DataFrame.describe(
    percentiles=None,
    include=None,
    exclude=None
)
```

---

# ⚙️ Parameters

| Parameter | Description | Default |
|-----------|-------------|---------|
| `percentiles` | List of percentiles to include | `[.25, .5, .75]` |
| `include` | Data types to include in the result | `None` (numeric only) |
| `exclude` | Data types to omit from the result | `None` |

---

# 💻 Example Dataset

```text
Employee_ID   Name      Age   Department   Salary
101           Ram       25    IT           50000
102           Ravi      28    HR           60000
103           John      30    Finance      70000
104           Priya     24    IT           55000
105           Anjali    27    Sales        52000
```

---

# 📌 Example 1 – Default Behavior (Numeric)

```python
import pandas as pd

df = pd.read_csv("employees.csv")

df.describe()
```

### Output

```text
               Age        Salary
count     5.000000      5.000000
mean     26.800000  57400.000000
std       2.387467   7861.297603
min      24.000000  50000.000000
25%      25.000000  52000.000000
50%      27.000000  55000.000000
75%      28.000000  60000.000000
max      30.000000  70000.000000
```

---

# 📌 Example 2 – Categorical Data

To view statistics for text data, use `include=['object']`.

```python
df.describe(include=['object'])
```

### Output

```text
         Name Department
count       5          5
unique      5          4
top       Ram         IT
freq        1          2
```

- `unique`: Number of distinct values.
- `top`: The most frequent value.
- `freq`: How many times the top value appears.

---

# 🏢 Real Industry Example

A Data Scientist loads house pricing data. 

They run `df.describe()` and look at the `Bedrooms` column. The 75% percentile says 4 bedrooms, but the `max` says 400 bedrooms. 

This instantly reveals a typo in the database. The scientist knows they must drop or fix that outlier before training a regression model.

---

# 🧠 Engineer Thinking

When reviewing `describe()`, ask yourself:

- Are the min/max values physically possible? (e.g., negative prices, ages over 120).
- Is the standard deviation abnormally large? (Indicates high variance or noise).
- Is the `mean` much higher than the `50%` (median)? If yes, the data is skewed by extremely high values.

---

# ⚡ Performance Notes

- `describe()` is very efficient, but for massive datasets with hundreds of numeric columns, it may take a moment to compute standard deviations and percentiles.

---

# ✅ Best Practices

- Always compare the `mean` and `50%` to check for skewness.
- Use `include='all'` to generate a single summary table containing both numeric and categorical data.
- Check for 0 minimums in columns where 0 doesn't make sense (like Age or Height), as 0 is often used as a lazy placeholder for missing data.

---

# ❌ Common Mistakes

### Mistake 1

Assuming `describe()` covers all columns by default.

It silently ignores `object` (text) and `datetime` columns unless explicitly told to include them.

---

### Mistake 2

Ignoring the count.

If the count is lower than your total row count, those missing values were ignored in the mean/std calculations, which might bias your understanding.

---

# 💼 Interview Questions

### Q1. What does `describe()` return for numeric data?

Count, mean, standard deviation, minimum, 25th percentile, median (50th), 75th percentile, and maximum.

---

### Q2. How can you find if a numeric column is heavily skewed?

By comparing the mean and the 50% (median). A large difference indicates skewness.

---

### Q3. What parameters do you pass to describe text columns?

`include=['object']` or `include='all'`.

---

# 📌 Summary

- `describe()` provides a statistical snapshot.
- It helps you find data entry errors and extreme outliers.
- You must use the `include` parameter to view categorical statistics.
- It is a foundational tool for feature engineering decisions (like scaling).

---

# 🚀 Next Topic

The next topic is:

**06-shape.md**

You'll learn how to extract the exact dimensions of your dataset programmatically, which is crucial for building robust automated data pipelines.
