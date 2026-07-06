# 🛡️ Module 03: Data Validation

Welcome to **Module 03: Data Validation**. 

Before you can clean or analyze data, you must verify that the data you have received meets the expected standards and rules of your business. Data validation is the process of ensuring data quality, accuracy, and integrity. If you skip validation, your machine learning models will learn from garbage data, leading to garbage predictions (GIGO - Garbage In, Garbage Out).

---

## 🎯 What You Will Learn

In this module, you will learn how to build robust validation checks to catch errors early in your data pipelines. We will cover everything from checking basic schemas and data types to enforcing complex business logic and consistency rules.

---

## 📂 Topics Covered

Here is the step-by-step roadmap for this module:

1. **[Schema Validation](01-Schema-Validation.md)** - Ensure your dataset has the correct columns and expected structure.
2. **[Data Type Validation](02-Data-Type-Validation.md)** - Verify that every column contains the correct and expected data types.
3. **[Missing Value Validation](03-Missing-Value-Validation.md)** - Detect and establish rules for the presence or absence of null values.
4. **[Duplicate Validation](04-Duplicate-Validation.md)** - Identify exact and partial duplicate records that could skew your data.
5. **[Business Key Validation](05-Business-Key-Validation.md)** - Ensure primary keys (like User IDs) are entirely unique.
6. **[Composite Key Validation](06-Composite-Key-Validation.md)** - Validate uniqueness across a combination of multiple columns.
7. **[Pattern Validation](07-Pattern-Validation.md)** - Use Regular Expressions (Regex) to validate text formats like emails, phone numbers, and zip codes.
8. **[Range Validation](08-Range-Validation.md)** - Ensure numerical and date values fall strictly within acceptable logical bounds.
9. **[Consistency Validation](09-Consistency-Validation.md)** - Check for logical contradictions between different columns in the exact same record.

---

## 🧠 Why is this important?

In the real world, data pipelines run automatically every single day. An engineer doesn't manually check the incoming data; instead, they write **Validation Tests**. If the daily data fails validation, the pipeline halts and triggers an alert *before* the bad data can corrupt the database or the Machine Learning models. 

This module will teach you how to think defensively and write code that expects data to fail.

Let's get started with **[01-Schema-Validation](01-Schema-Validation.md)**!
