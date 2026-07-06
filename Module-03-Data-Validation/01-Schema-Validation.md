 
# Schema Validation

## 📖 What is Schema Validation?

Schema Validation is the process of verifying that a dataset follows the expected structure before performing any analysis or training a Machine Learning model.

A schema defines:

- Column names
- Data types
- Required columns
- Optional columns
- Value constraints

If the dataset does not follow the expected schema, it should be corrected before further processing.

---

## 🤔 Why is Schema Validation Important?

Imagine you built an ML model using this dataset.

| Name | Age | Salary |
|------|----:|-------:|
| Ravi | 25 | 40000 |

Next month, another team sends:

| Name | Age | SalaryAmount |
|------|----:|-------------:|
| Ravi | 25 | 40000 |

Your code expects:

```python
df["Salary"]
```

Instead, the dataset contains:

```python
SalaryAmount
```

Result:

```text
KeyError: 'Salary'
```

The entire pipeline fails.

Schema validation helps detect these issues before processing begins.

---

# What Does Schema Validation Check?

A schema validation process typically checks:

- Required columns exist
- Column names are correct
- Data types are correct
- No unexpected columns
- Missing required columns
- Data format is valid

---

# Real World Example

Suppose your ML model expects:

| Column | Data Type |
|---------|-----------|
| Name | object |
| Age | int |
| Salary | float |

Incoming dataset:

| Name | Age | Salary |
|------|------|--------|
| Ravi | "Twenty Five" | 40000 |

Problem:

Age should be integer.

Actual value:

```text
"Twenty Five"
```

Schema validation detects this before model training.

---

# Checking Required Columns

```python
required_columns = ["Name", "Age", "Salary"]

missing = set(required_columns) - set(df.columns)

if missing:
    print("Missing Columns:", missing)
else:
    print("Schema Valid")
```

---

# Checking Data Types

```python
print(df.dtypes)
```

Expected:

```text
Name      object
Age        int64
Salary   float64
```

---

# Why Companies Perform Schema Validation

In production systems:

Daily

↓

New CSV Files

↓

Validate Schema

↓

Data Cleaning

↓

Feature Engineering

↓

Model Prediction

Without schema validation, production pipelines may fail.

---

# Common Errors Found

- Missing columns
- Extra columns
- Wrong column names
- Wrong data types
- Empty datasets
- Invalid values

---

# Interview Question

### What is Schema Validation?

Answer:

Schema validation is the process of verifying that a dataset matches the expected structure, including column names, data types, and required fields before further processing.

---

# Best Practices

✅ Validate schema before cleaning.

✅ Check required columns.

✅ Verify data types.

✅ Standardize column names.

✅ Stop processing if critical columns are missing.

---

# Summary

Schema Validation ensures that incoming data matches the expected format before data cleaning, feature engineering, and machine learning model training.