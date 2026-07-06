 
# Pattern Validation

## 📌 Overview

Pattern Validation is the process of verifying that values follow a predefined format or pattern.

Many business fields such as Email Address, Phone Number, PAN Number, Aadhaar Number, ZIP Code, Passport Number, and Vehicle Registration Number must follow a standard format.

Pattern Validation ensures that only correctly formatted data enters the system.

---

# Why Pattern Validation is Important

Incorrect formats can cause:

- Invalid customer records
- Communication failures
- Database inconsistencies
- Data processing errors
- Machine Learning preprocessing failures

Pattern validation helps identify these issues before analysis.

---

# Real World Example

Customer Dataset

| Customer_ID | Email | Phone |
|-------------|----------------|------------|
| C101 | ravi@gmail.com | 9876543210 |
| C102 | priya.gmail.com | 98765AB210 |
| C103 | rahul@yahoo.com | 9123456789 |

Problems

- Email is missing '@'
- Phone contains alphabets

These records fail Pattern Validation.

---

# Common Pattern Validations

| Field | Expected Pattern |
|--------|------------------|
| Email | user@example.com |
| Phone | 10 Digits |
| Aadhaar | 12 Digits |
| PAN | ABCDE1234F |
| Passport | Alphanumeric |
| ZIP Code | 6 Digits |

---

# Email Validation

```python
email_pattern = r'^[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\.[A-Za-z]{2,}$'

df["Email"].str.match(email_pattern)
```

---

# Phone Number Validation

```python
phone_pattern = r'^[0-9]{10}$'

df["Phone"].str.match(phone_pattern)
```

---

# Find Invalid Records

```python
invalid_email = df[
    ~df["Email"].str.match(email_pattern)
]
```

---

# Best Practices

- Validate important business fields.
- Use Regular Expressions (Regex).
- Keep validation rules configurable.
- Flag invalid records for review.

---

# Interview Question

### What is Pattern Validation?

Pattern Validation verifies that values follow a predefined format using validation rules or Regular Expressions (Regex).

---

# Practice Exercise

Dataset

| Email | Phone |
|------------------|------------|
| ravi@gmail.com | 9876543210 |
| ravi.gmail.com | 98765AB210 |
| abc@yahoo.com | 9123456789 |

Questions

1. Which email is invalid?
2. Which phone number is invalid?
3. Which Python concept is commonly used for Pattern Validation?

---

# Key Takeaways

- Pattern Validation checks data format.
- Regex is widely used.
- Email, Phone, PAN, Passport and Aadhaar are common validation examples.