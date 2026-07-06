# Missing Value Validation

## 📌 Overview

Missing Value Validation is the process of identifying and analyzing missing (null) values in a dataset before performing data cleaning, analysis, or training a Machine Learning model.

Missing values are one of the most common data quality issues. If they are not handled properly, they can reduce model accuracy, produce incorrect insights, or even cause some Machine Learning algorithms to fail.

---

# Why Missing Value Validation is Important

Before cleaning missing values, we must first identify:

- Which columns contain missing values?
- How many missing values exist?
- What percentage of the dataset is missing?
- Is the missing data acceptable?
- Should the missing values be removed or imputed?

Answering these questions helps us choose the correct preprocessing technique.

---

# Real World Example

Suppose an Employee dataset contains the following data.

| Name | Age | Salary | Department |
|------|-----|---------|------------|
| Ravi | 25 | 45000 | IT |
| Priya | NaN | 52000 | HR |
| Rahul | 30 | NaN | IT |
| Sneha | 28 | 48000 | NaN |

Here,

- Age contains one missing value.
- Salary contains one missing value.
- Department contains one missing value.

These missing values should be identified before further processing.

---

# How to Detect Missing Values

## Check Missing Values in Every Column

```python
df.isnull().sum()
```

Output

```text
Name          0
Age           1
Salary        1
Department    1
dtype: int64
```

This shows the number of missing values in each column.

---

## Check Total Missing Values

```python
df.isnull().sum().sum()
```

Output

```text
3
```

Meaning the entire dataset contains three missing values.

---

## Check if Dataset Contains Missing Values

```python
df.isnull().values.any()
```

Output

```text
True
```

If no missing values exist, the output will be:

```text
False
```

---

# Calculate Missing Value Percentage

Knowing the percentage of missing values helps in deciding whether to remove or impute data.

```python
(df.isnull().sum() / len(df)) * 100
```

Example Output

```text
Name           0%
Age           25%
Salary        25%
Department    25%
```

---

# Visualizing Missing Values

Sometimes visualization makes missing values easier to understand.

```python
import seaborn as sns

sns.heatmap(df.isnull())
```

This highlights missing values visually.

---

# Common Reasons for Missing Values

- User skipped entering data.
- Sensor failed to collect data.
- Data corruption during transfer.
- System or database errors.
- Incorrect data import.

---

# What Should We Do After Validation?

After identifying missing values, we decide whether to:

- Remove rows
- Remove columns
- Fill with Mean
- Fill with Median
- Fill with Mode
- Use Forward Fill or Backward Fill
- Apply Advanced Imputation Techniques

The appropriate method depends on the data and business requirements.

---

# Best Practices

- Always check missing values immediately after loading the dataset.
- Calculate both the count and percentage of missing values.
- Understand why data is missing before handling it.
- Avoid deleting data without proper analysis.
- Document every missing value treatment performed.

---

# Interview Questions

### What is Missing Value Validation?

**Answer:**

Missing Value Validation is the process of identifying null or missing values in a dataset before preprocessing. It helps ensure data quality and determines the appropriate strategy for handling incomplete data.

---

### Which Pandas function is commonly used to detect missing values?

**Answer:**

```python
df.isnull().sum()
```

This returns the number of missing values in each column.

---

### Why should we validate missing values before training a Machine Learning model?

**Answer:**

Missing values can cause incorrect analysis, reduce model accuracy, and may prevent some Machine Learning algorithms from working properly. Validating missing values ensures the dataset is suitable for preprocessing and model training.

---

# Practice Exercise

Consider the following dataset.

| Name | Age | Salary | Department |
|------|-----|---------|------------|
| Ravi | 25 | 45000 | IT |
| Priya | NaN | 52000 | HR |
| Rahul | 30 | NaN | IT |
| Sneha | NaN | 48000 | NaN |

Answer the following:

1. Which columns contain missing values?
2. How many missing values are present in each column?
3. Which Pandas function is used to detect missing values?
4. Which columns would require data cleaning?

---

# Key Takeaways

- Missing Value Validation is the first step before handling null values.
- Use `df.isnull().sum()` to identify missing values in each column.
- Use `df.isnull().sum().sum()` to find the total number of missing values.
- Calculate the percentage of missing values before deciding on a cleaning strategy.
- Validate missing values before feature engineering and Machine Learning model training.