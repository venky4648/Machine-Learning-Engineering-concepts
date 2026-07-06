 # Data Type Validation

## 📌 Overview

Data Type Validation is the process of verifying that every column in a dataset has the expected data type before performing data analysis or training a Machine Learning model.

Every dataset has a predefined schema, where each column is expected to store a specific type of data. If a column contains an incorrect data type, it can lead to incorrect analysis, runtime errors, or poor model performance.

---

# Why Data Type Validation is Important

Machine Learning algorithms expect data in a specific format.

For example:

| Column | Expected Data Type |
|----------|-------------------|
| Name | String (object) |
| Age | Integer |
| Salary | Float |
| Joining_Date | Datetime |
| Is_Active | Boolean |

If the actual data type is different from the expected one, the data should be corrected before moving to the next stage of the pipeline.

---

# Real World Example

Consider an Employee dataset.

| Name | Age | Salary |
|------|-----|---------|
| Ravi | 25 | 45000 |
| Priya | Twenty Six | 52000 |
| Rahul | 30 | Fifty Thousand |

Expected Data Types

| Column | Expected |
|----------|----------|
| Name | object |
| Age | int |
| Salary | float |

Problems

- Age contains text ("Twenty Six")
- Salary contains text ("Fifty Thousand")

These values cannot be used directly for numerical analysis or Machine Learning.

---

# How to Check Data Types

Pandas provides the `dtypes` attribute to inspect the data type of every column.

```python
import pandas as pd

df = pd.read_csv("employees.csv")

print(df.dtypes)
```

Output

```text
Name       object
Age         int64
Salary    float64
dtype: object
```

---

# Understanding Common Pandas Data Types

| Data Type | Description | Example |
|------------|-------------|----------|
| object | Text/String | Ravi |
| int64 | Integer | 25 |
| float64 | Decimal Number | 45000.75 |
| bool | True or False | True |
| datetime64 | Date and Time | 2025-07-01 |

---

# Checking a Single Column Data Type

```python
print(df["Salary"].dtype)
```

Output

```text
float64
```

---

# Converting Data Types

Sometimes the dataset contains correct values but the wrong data type.

Example

| Salary |
|---------|
| "45000" |
| "52000" |
| "61000" |

Current Type

```text
object
```

Convert into integer

```python
df["Salary"] = df["Salary"].astype(int)
```

---

# Safe Conversion

If a column contains invalid values, use `pd.to_numeric()`.

```python
df["Salary"] = pd.to_numeric(
    df["Salary"],
    errors="coerce"
)
```

Invalid values become

```text
NaN
```

instead of raising an error.

---

# Date Type Validation

```python
df["Joining_Date"] = pd.to_datetime(
    df["Joining_Date"],
    errors="coerce"
)
```

Invalid dates automatically become

```text
NaT
```

(Not a Time)

---

# Common Data Type Validation Errors

- Numbers stored as text
- Dates stored as strings
- Boolean values stored as "Yes" / "No"
- Mixed data types in a single column
- Invalid numeric values

---

# Best Practices

- Always inspect data types after loading a dataset.
- Convert columns to appropriate data types before analysis.
- Use `pd.to_numeric()` and `pd.to_datetime()` with `errors="coerce"` for safe conversion.
- Validate data types before feature engineering and model training.

---

# Interview Question

### What is Data Type Validation?

**Answer:**

Data Type Validation is the process of verifying that each column contains the correct data type according to the expected schema. It ensures data consistency and prevents errors during analysis and Machine Learning.

---

### Why is Data Type Validation important?

**Answer:**

Incorrect data types can cause calculation errors, model failures, incorrect aggregations, and poor prediction accuracy. Validating and converting data types ensures reliable preprocessing and model performance.

---

# Practice Exercise

Given the following dataset:

| Name | Age | Salary | Joining_Date |
|------|-----|---------|--------------|
| Ravi | 25 | 45000 | 2025-01-15 |
| Priya | Twenty Six | 52000 | 15/01/2025 |
| Rahul | 30 | Fifty Thousand | Invalid Date |

Identify:

1. Which columns contain incorrect data types?
2. Which Pandas function would you use to validate the data types?
3. Which function would you use to safely convert numeric columns?
4. Which function would you use to safely convert date columns?

---

# Key Takeaways

- Data Type Validation ensures that every column has the expected data type.
- Use `df.dtypes` to inspect column data types.
- Use `astype()` for direct conversion when data is clean.
- Use `pd.to_numeric()` for safe numeric conversion.
- Use `pd.to_datetime()` for safe date conversion.
- Always validate data types before performing analysis or training Machine Learning models.
