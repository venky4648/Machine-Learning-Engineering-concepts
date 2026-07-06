 
# Range Validation

## 📌 Overview

Range Validation is the process of ensuring that numerical or date values fall within an acceptable minimum and maximum range.

It helps detect unrealistic values before analysis or Machine Learning.

---

# Why Range Validation is Important

Invalid numerical values produce incorrect analysis and poor ML models.

Examples

- Age = -5
- Salary = -10000
- Marks = 120
- Rating = 7 (Allowed: 1–5)

These values violate business rules.

---

# Real World Example

Employee Dataset

| Name | Age | Salary |
|------|-----|---------|
| Ravi | 25 | 45000 |
| Priya | -8 | 50000 |
| Rahul | 140 | 60000 |

Problems

- Negative age
- Unrealistic age

---

# Validate Age

```python
invalid_age = df[
    (df["Age"] < 18) |
    (df["Age"] > 60)
]
```

---

# Validate Salary

```python
invalid_salary = df[
    df["Salary"] < 0
]
```

---

# Validate Marks

```python
invalid_marks = df[
    (df["Marks"] < 0) |
    (df["Marks"] > 100)
]
```

---

# Common Range Validations

| Field | Valid Range |
|--------|-------------|
| Age | 18 – 60 |
| Marks | 0 – 100 |
| Salary | > 0 |
| Rating | 1 – 5 |
| Attendance | 0 – 100 |

---

# Best Practices

- Define business limits.
- Validate numeric columns immediately.
- Investigate invalid values before removing them.
- Keep validation rules configurable.

---

# Interview Question

### What is Range Validation?

Range Validation ensures that numerical or date values fall within an acceptable minimum and maximum range defined by business rules.

---

# Practice Exercise

Dataset

| Age | Marks |
|-----|-------|
|25|90|
|-5|80|
|150|75|
|30|110|

Questions

1. Which rows fail Age validation?
2. Which rows fail Marks validation?
3. Why is Range Validation important?

---

# Key Takeaways

- Prevents unrealistic values.
- Uses minimum and maximum limits.
- Improves data quality before ML.