# 🏷️ columns in Pandas

> The `columns` attribute allows you to access and manipulate the column names of your DataFrame. Messy column names are a major source of bugs in data pipelines, making this attribute essential for data cleaning.

---

# 📖 Table of Contents

1. Introduction
2. Learning Objectives
3. What is `columns`?
4. Why Do We Use `columns`?
5. Syntax
6. Parameters
7. Examples
8. Output
9. Industry Example
10. Engineer Thinking
11. Best Practices
12. Common Mistakes
13. Interview Questions
14. Summary
15. Next Topic

---

# 🎯 Learning Objectives

After completing this topic, you will be able to:

- Access the column labels of a DataFrame.
- Identify poorly formatted column names.
- Clean and standardize column names using Python string methods.
- Rename specific columns safely.

---

# 📘 What is `columns`?

`columns` is an **attribute** (not a function) of a Pandas DataFrame.

It returns an Index object containing the labels (names) of all the columns in the dataset.

---

# ❓ Why Do We Use `columns`?

Real-world data often comes from legacy systems, spreadsheets, or manually entered forms. This leads to column names with:

- Leading or trailing spaces (`" Age "`)
- Mixed capitalization (`"firstName"`, `"LastName"`)
- Special characters (`"Salary ($)"`)

You use `columns` to inspect these names and standardize them so that calling `df['age']` doesn't throw a `KeyError`.

---

# 📝 Syntax

```python
# To access column names
DataFrame.columns

# To reassign column names
DataFrame.columns = [list_of_new_names]
```

---

# ⚙️ Parameters

Since `columns` is an attribute, it takes **no parameters**.

---

# 💻 Example Dataset

```text
First Name   |  Age  | Salary ($) | department_id
Ram          |  25   | 50000      | 1
Ravi         |  28   | 60000      | 2
```

---

# 📌 Example 1 – Default Behavior

```python
import pandas as pd

df = pd.read_csv("messy_data.csv")

print(df.columns)
```

### Output

```text
Index(['First Name ', '  Age', 'Salary ($)', 'department_id'], dtype='object')
```

Notice the hidden spaces and inconsistent formatting!

---

# 📌 Example 2 – Standardizing Column Names

You can overwrite the `columns` attribute directly.

```python
# Convert to lowercase and replace spaces with underscores
df.columns = df.columns.str.strip().str.lower().str.replace(' ', '_')

print(df.columns)
```

### Output

```text
Index(['first_name', 'age', 'salary_($)', 'department_id'], dtype='object')
```

---

# 🏢 Real Industry Example

A Data Scientist downloads a dataset with 150 columns from an enterprise SQL database. 

Instead of typing out all 150 names, they write a quick list comprehension using `df.columns` to sanitize everything instantly:

```python
import re

# Remove any non-alphanumeric character and convert to snake_case
df.columns = [re.sub(r'[^a-zA-Z0-9_]', '', col.lower().replace(' ', '_')) for col in df.columns]
```

This single line of code prevents hundreds of `KeyError` bugs downstream.

---

# 🧠 Engineer Thinking

When inspecting `columns`, ask yourself:

- Are the names standardized? (Usually, `snake_case` is preferred in Python).
- Are there trailing spaces that I can't easily see?
- Do any columns have identical names? (Pandas handles duplicate column names poorly).

---

# ⚡ Performance Notes

- Accessing `columns` is instantaneous, as it just reads the index object stored in memory.

---

# ✅ Best Practices

- Standardize column names as the **very first step** of your data cleaning pipeline.
- Use `snake_case` (lowercase with underscores) for all columns. It makes typing easier and plays nicely with code auto-completion tools.
- Use the `rename()` method if you only need to change one or two specific columns, rather than overwriting the whole `df.columns` array.

---

# ❌ Common Mistakes

### Mistake 1

Trying to call it like a function.

```python
# Error!
df.columns() 
```

`TypeError: 'Index' object is not callable`

---

### Mistake 2

Forgetting to strip leading/trailing spaces.

```python
df['Age'] # Raises KeyError if the column is actually ' Age '
```

---

# 💼 Interview Questions

### Q1. How do you list all column names in a DataFrame?

By accessing the `df.columns` attribute.

---

### Q2. How can you programmatically convert all column names to lowercase?

By reassigning the attribute: `df.columns = df.columns.str.lower()`

---

### Q3. Why is it recommended to remove spaces from column names?

Spaces can cause bugs, are easily missed visually, and prevent you from accessing columns using dot notation (e.g., `df.age` works, `df.Age (Years)` does not).

---

# 📌 Summary

- `columns` is an attribute that returns column labels.
- Messy columns cause `KeyError` exceptions.
- You can use Pandas string methods (`.str`) or list comprehensions to sanitize column names efficiently.

---

# 🚀 Next Topic

The next topic is:

**08-index.md**

You'll learn about DataFrame row labels (the Index), how they function, and how to optimize data lookups.
