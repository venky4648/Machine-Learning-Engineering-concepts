
# Duplicate Validation

## 📌 Overview

Duplicate Validation is the process of identifying repeated records in a dataset before performing data analysis or training a Machine Learning model.

Duplicate records can lead to incorrect statistics, biased models, and inaccurate business insights.

---

# Why Duplicate Validation is Important

Duplicate records can:

- Increase dataset size unnecessarily.
- Bias Machine Learning models.
- Produce incorrect aggregations.
- Reduce overall data quality.
- Generate misleading business reports.

Therefore, duplicates should always be identified and reviewed before preprocessing.

---

# Real World Example

Suppose an Employee dataset.

| Employee_ID | Name | Department | Salary |
|--------------|------|------------|---------|
| 101 | Ravi | IT | 45000 |
| 102 | Priya | HR | 52000 |
| 101 | Ravi | IT | 45000 |

The third row is an exact duplicate of the first row.

If this duplicate remains,

- Employee count becomes incorrect.
- Average salary calculations become inaccurate.
- Reports become misleading.

---

# Detect Duplicate Rows

```python
df.duplicated()
```

Output

```text
0    False
1    False
2     True
```

---

# Count Duplicate Rows

```python
df.duplicated().sum()
```

Output

```text
1
```

---

# Display Duplicate Records

```python
duplicates = df[df.duplicated()]
print(duplicates)
```

---

# Remove Duplicate Records

```python
df = df.drop_duplicates()
```

---

# Remove Duplicates Based on Specific Columns

```python
df.drop_duplicates(subset=["Employee_ID"])
```

---

# Common Causes of Duplicate Data

- Manual data entry
- Multiple system imports
- Database synchronization issues
- Incorrect merge operations
- User submitting the same form multiple times

---

# Best Practices

- Always check duplicates after loading the dataset.
- Verify whether duplicates are valid before removing them.
- Remove duplicates using business keys whenever possible.
- Never remove duplicates without understanding the business context.

---

# Interview Questions

### What is Duplicate Validation?

Duplicate Validation is the process of identifying repeated records within a dataset to ensure data quality and prevent inaccurate analysis.

---

### Which Pandas function detects duplicate rows?

```python
df.duplicated()
```

---

### Which function removes duplicate rows?

```python
df.drop_duplicates()
```

---

# Practice Exercise

Dataset

| Employee_ID | Name | Department |
|--------------|------|------------|
|101|Ravi|IT|
|102|Priya|HR|
|101|Ravi|IT|
|103|Rahul|Finance|

Questions

1. How many duplicate rows exist?
2. Which Pandas function detects duplicates?
3. Which function removes duplicate rows?

---

# Key Takeaways

- Detect duplicates before analysis.
- Use `duplicated()` to identify duplicate records.
- Use `drop_duplicates()` to remove duplicates.
- Always validate duplicates using business requirements.