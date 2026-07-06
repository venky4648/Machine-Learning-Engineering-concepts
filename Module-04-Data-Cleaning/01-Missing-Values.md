# 🕳️ Missing Values in Pandas

> Missing values (`NaN`, `None`, `Null`) are the most common data issue you will encounter. Handling them incorrectly can completely ruin a Machine Learning model. 

---

# 📖 Table of Contents

1. Introduction
2. Learning Objectives
3. What are Missing Values?
4. Why Do We Care About Missing Values?
5. Syntax & Detection
6. Handling Strategies
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

- Detect missing values in a dataset.
- Understand the difference between dropping data and imputing data.
- Use `dropna()` to remove missing values safely.
- Use `fillna()` to replace missing values with statistical measures (mean, median, mode).

---

# 📘 What are Missing Values?

A missing value occurs when no data is stored for a variable in an observation. 

In Pandas, missing values are typically represented by `NaN` (Not a Number), which comes from the NumPy library. 

---

# ❓ Why Do We Care About Missing Values?

Most Machine Learning algorithms (like Scikit-Learn's Linear Regression or Random Forest) **cannot handle missing values natively**. If you pass a dataset with even one `NaN` into these models, they will throw an error and crash.

You MUST either remove them or guess them (impute) before training.

---

# 📝 Syntax & Detection

Before fixing missing values, you must find them.

```python
# Check for null values (returns boolean mask)
df.isnull() 
df.isna()

# Get total missing values per column
df.isnull().sum()
```

---

# ⚙️ Handling Strategies

You have two main choices:

1. **Deletion (`dropna`)**: Remove the row or column.
2. **Imputation (`fillna`)**: Fill the missing spot with a substitute value (mean, median, mode, or a constant).

---

# 💻 Example Dataset

```text
Employee_ID   Name      Age   Salary
101           Ram       25    50000
102           Ravi      NaN   60000
103           John      30    NaN
104           Priya     24    55000
```

---

# 📌 Example 1 – Dropping Missing Values

If a row is missing critical data, you might just drop it entirely.

```python
import pandas as pd

df = pd.read_csv("employees.csv")

# Drops any row that contains at least one NaN
df_cleaned = df.dropna()

print(df_cleaned)
```

### Output

```text
   Employee_ID   Name   Age   Salary
0          101    Ram  25.0  50000.0
3          104  Priya  24.0  55000.0
```
Notice how rows 102 and 103 were completely removed.

---

# 📌 Example 2 – Imputing (Filling) Missing Values

Instead of throwing away data, we can fill the missing values with the **Median** or **Mean**.

```python
# Fill missing Age with the median age
median_age = df['Age'].median()
df['Age'] = df['Age'].fillna(median_age)

# Fill missing Salary with 0 (Constant Imputation)
df['Salary'] = df['Salary'].fillna(0)
```

---

# 🏢 Real Industry Example

A Data Scientist receives a dataset of 100,000 houses to predict house prices. The `Square_Footage` column has 500 missing values (0.5% of the data). 
Because the missing percentage is so low, they simply use `df.dropna(subset=['Square_Footage'])` to drop those specific 500 rows. 

However, the `Pool_Size` column is missing in 90% of the rows (because most houses don't have pools). Instead of dropping 90% of the data, they fill the missing values with `0`, representing "No Pool".

---

# 🧠 Engineer Thinking

When facing missing values, ask yourself:

- **Why is it missing?** (Was it an entry error, or does 'Missing' actually mean something, like 'No Pool'?)
- **How much is missing?** (If a column is 95% missing, drop the column. If 1% is missing, drop the rows or impute).
- **Should I use Mean or Median?** (If the data has extreme outliers, the Mean is skewed, so you must use the Median).

---

# ⚡ Performance Notes

- Imputing using `.fillna()` is generally very fast.
- Be careful with `inplace=True`. It's often better to explicitly overwrite the column `df['Col'] = df['Col'].fillna(val)` to avoid chained assignment warnings in Pandas.

---

# ✅ Best Practices

- Check the percentage of missing values per column `(df.isnull().sum() / len(df)) * 100`.
- Impute Categorical data using the Mode (most frequent value) or a constant like `"Unknown"`.
- Never impute target variables (the thing you are trying to predict). If the target is missing, drop the row.

---

# ❌ Common Mistakes

### Mistake 1

Filling missing values before splitting your data into Train and Test sets.

**Data Leakage**: If you calculate the Mean of the entire dataset and fill NaNs, information from your Test set has "leaked" into your training data! You must split the data *first*, calculate the Mean on the Train set, and apply that Mean to both sets.

---

# 💼 Interview Questions

### Q1. How do you find the number of missing values in each column?
`df.isnull().sum()`

---

### Q2. When should you use Mean imputation vs Median imputation?
Use Mean when the data is normally distributed. Use Median when the data is skewed or contains extreme outliers, because the Median is robust to outliers.

---

### Q3. What is Data Leakage in the context of missing values?
Calculating imputation statistics (like the mean) on the entire dataset before doing a train-test split, allowing the test data to influence the training data.

---

# 📌 Summary

- Missing values (`NaN`) break Machine Learning models.
- Find them with `isnull().sum()`.
- Drop them with `dropna()` if the missing percentage is very small.
- Fill them with `fillna()` using Mean, Median, or Mode if you need to retain the data.

---

# 🚀 Next Topic

The next topic is:

**02-Duplicate-Removal.md**

You'll learn how to identify and safely remove duplicate rows, which can artificially skew your model's perception of reality.
