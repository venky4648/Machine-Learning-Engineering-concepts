 
# Consistency Validation

## 📌 Overview

Consistency Validation is the process of verifying that related columns do not contradict each other and satisfy business rules.

A record may contain valid individual values, but together those values may become logically incorrect.

Consistency Validation identifies such inconsistencies.

---

# Why Consistency Validation is Important

Many columns are related.

If their values contradict each other, business decisions and ML predictions become unreliable.

Consistency Validation ensures logical correctness across multiple columns.

---

# Real World Example 1

Employee Dataset

| Joining_Date | Resignation_Date |
|--------------|------------------|
|2024-01-10|2025-06-20|
|2025-05-01|2024-12-15|

Problem

The employee resigned before joining.

This violates Consistency Validation.

---

# Real World Example 2

Student Dataset

| Marks | Result |
|-------|--------|
|90|Fail|
|30|Pass|

Problem

Marks and Result contradict each other.

---

# Real World Example 3

Employee Dataset

| Age | Experience |
|-----|------------|
|22|18|
|20|15|

A 20-year-old employee cannot realistically have 15 years of experience.

---

# Validate Joining and Resignation Date

```python
invalid = df[
    df["Joining_Date"] > df["Resignation_Date"]
]
```

---

# Validate Marks and Result

```python
invalid = df[
    (df["Marks"] >= 35) &
    (df["Result"] == "Fail")
]
```

---

# Common Consistency Rules

- Joining Date < Resignation Date
- Start Date < End Date
- Age > Experience
- Marks and Result should match
- Order Status and Payment Status should be consistent

---

# Best Practices

- Understand business rules first.
- Compare related columns.
- Flag inconsistent records.
- Review records before removing them.

---

# Interview Question

### What is Consistency Validation?

Consistency Validation verifies that related fields do not contradict each other and satisfy business logic.

---

# Practice Exercise

Dataset

| Joining_Date | Resignation_Date |
|--------------|------------------|
|2024-01-01|2025-05-01|
|2025-03-01|2024-12-20|

Questions

1. Which row violates the business rule?
2. Why is it inconsistent?
3. How would you validate it using Pandas?

---

# Key Takeaways

- Checks logical relationships between columns.
- Based on business rules.
- Prevents contradictory records.
- Improves overall data quality.