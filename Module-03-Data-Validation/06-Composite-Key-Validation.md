 
# Composite Key Validation

## 📌 Overview

Composite Key Validation ensures that the combination of two or more columns uniquely identifies each record.

Sometimes a single column is not sufficient to uniquely identify data.

In such cases, multiple columns together form a Composite Key.

---

# Why Composite Keys are Needed

Consider Student Marks.

| Student_ID | Subject | Marks |
|-------------|----------|-------|
|101|Math|95|
|101|Science|90|

Student_ID repeats because one student has multiple subjects.

Similarly,

Subject also repeats.

Neither column is unique individually.

However,

Student_ID + Subject

uniquely identifies each record.

This is called a Composite Key.

---

# Real World Examples

| Business | Composite Key |
|-----------|---------------|
| Student Marks | Student_ID + Subject |
| Order Details | Order_ID + Product_ID |
| Flight Booking | Flight_No + Seat_No |
| Employee Attendance | Employee_ID + Date |

---

# Detect Duplicate Composite Keys

```python
df[df.duplicated(subset=["Student_ID", "Subject"])]
```

---

# Count Duplicate Composite Keys

```python
df.duplicated(
    subset=["Student_ID", "Subject"]
).sum()
```

---

# Example

| Student_ID | Subject |
|-------------|----------|
|101|Math|
|101|Science|
|101|Math|

Duplicate

```text
Student_ID = 101

Subject = Math
```

Composite Key is duplicated.

---

# Best Practices

- Identify whether one column is sufficient.
- If not, combine multiple columns.
- Validate uniqueness using duplicated(subset=[]).

---

# Interview Question

### What is a Composite Key?

A Composite Key is a combination of two or more columns that together uniquely identify a record.

---

### How do you validate Composite Keys in Pandas?

```python
df.duplicated(subset=["Column1", "Column2"])
```

---

# Practice Exercise

Dataset

| Order_ID | Product_ID | Quantity |
|-----------|------------|----------|
|101|P1|2|
|101|P2|1|
|101|P1|5|

Questions

1. Which columns form the Composite Key?
2. Is the Composite Key unique?
3. Which Pandas function validates Composite Keys?

---

# Key Takeaways

- Composite Keys combine multiple columns.
- Use `duplicated(subset=[...])` for validation.
- Composite Keys are common in transactional datasets.
- Validate Composite Keys before analysis and database insertion.