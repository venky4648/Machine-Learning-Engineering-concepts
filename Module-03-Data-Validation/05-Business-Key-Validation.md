 
# Business Key Validation

## 📌 Overview

Business Key Validation ensures that the business identifier used to uniquely identify a record does not contain duplicate values.

Unlike a Primary Key, a Business Key has real-world business meaning.

Examples include:

- Employee ID
- Email Address
- Aadhaar Number
- Passport Number
- Product Code

Each business key should uniquely identify one record.

---

# Why Business Key Validation is Important

Duplicate business keys indicate data quality issues.

For example,

Two employees should never share the same Employee ID.

If duplicates exist,

- Employee records become unreliable.
- Reports become inconsistent.
- Business operations may fail.

---

# Real World Example

| Employee_ID | Name |
|--------------|------|
|EMP101|Ravi|
|EMP102|Priya|
|EMP101|Rahul|

Problem

Employee_ID "EMP101" appears twice.

This violates Business Key Validation.

---

# Detect Duplicate Business Keys

```python
df[df["Employee_ID"].duplicated()]
```

---

# Count Duplicate Business Keys

```python
df["Employee_ID"].duplicated().sum()
```

---

# Validate Uniqueness

```python
df["Employee_ID"].is_unique
```

Output

```text
True
```

or

```text
False
```

---

# Real World Business Keys

- Employee_ID
- Customer_ID
- Product_Code
- Invoice_Number
- Passport_Number
- Aadhaar_Number

---

# Best Practices

- Every Business Key should be unique.
- Never allow duplicate business identifiers.
- Validate uniqueness before database insertion.

---

# Interview Question

### What is a Business Key?

A Business Key is a business-specific attribute used to uniquely identify a record. Unlike surrogate keys, it has real-world meaning.

---

# Practice Exercise

Dataset

| Customer_ID | Name |
|--------------|------|
|C101|Ravi|
|C102|Priya|
|C101|Rahul|

Questions

1. Which column is the Business Key?
2. Is it unique?
3. Which Pandas function checks uniqueness?

---

# Key Takeaways

- Business Keys represent real-world identifiers.
- Validate uniqueness before processing.
- Duplicate Business Keys indicate data quality issues.