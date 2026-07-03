# 📄 Reading CSV Files in Pandas

> CSV (Comma-Separated Values) is the most widely used file format in Data Science, Machine Learning, Data Engineering, and Analytics. Learning how to efficiently read CSV files is one of the first and most essential skills for every Machine Learning Engineer.

---

# 📖 Table of Contents

1. What is a CSV File?
2. Why Do We Use CSV Files?
3. Advantages of CSV
4. Common Use Cases
5. Reading a CSV File
6. Important Parameters of `read_csv()`
7. Examples
8. Best Practices
9. Common Errors
10. Interview Questions
11. Summary

---

# 🎯 Learning Objectives

After completing this topic, you will be able to:

- Understand the CSV file format.
- Load CSV files using Pandas.
- Use important `read_csv()` parameters.
- Handle common CSV loading issues.
- Apply best practices used in industry.

---

# 📘 What is a CSV File?

CSV stands for **Comma-Separated Values**.

It is a plain text file where each row represents a record and each column is separated by a comma.

Example:

```csv
Employee_ID,Name,Age,Salary
101,Ram,25,50000
102,Ravi,28,60000
103,John,30,70000
```

---

# 🏢 Why Do Companies Use CSV?

CSV files are:

- Lightweight
- Easy to read
- Human-readable
- Supported by almost every programming language
- Compatible with Excel, SQL, Python, R, Java, etc.

Most datasets available on platforms like Kaggle are provided in CSV format.

---

# 📦 Installing Pandas

```bash
pip install pandas
```

---

# 📥 Import Pandas

```python
import pandas as pd
```

---

# 📂 Reading a CSV File

```python
import pandas as pd

df = pd.read_csv("employees.csv")
```

Explanation:

- `pd` → Alias for Pandas
- `read_csv()` → Reads a CSV file
- `employees.csv` → File name
- `df` → DataFrame containing the loaded data

---

# 📊 Example Dataset

employees.csv

```csv
Employee_ID,Name,Age,Department,Salary
101,Ram,25,IT,50000
102,Ravi,28,HR,60000
103,John,30,Finance,70000
```

Python Code

```python
import pandas as pd

df = pd.read_csv("employees.csv")

print(df)
```

Output

```text
   Employee_ID  Name  Age Department  Salary
0          101   Ram   25         IT   50000
1          102  Ravi   28         HR   60000
2          103  John   30    Finance   70000
```

---

# ⚙️ Important Parameters

## 1. header

Specifies which row should be used as column names.

```python
pd.read_csv("employees.csv", header=0)
```

---

## 2. names

Assign custom column names.

```python
columns = [
    "ID",
    "Name",
    "Age",
    "Department",
    "Salary"
]

df = pd.read_csv(
    "employees.csv",
    names=columns
)
```

---

## 3. usecols

Load only specific columns.

```python
df = pd.read_csv(
    "employees.csv",
    usecols=["Name", "Salary"]
)
```

Why use it?

- Faster loading
- Lower memory usage
- Better performance for large datasets

---

## 4. nrows

Read only the first few rows.

```python
df = pd.read_csv(
    "employees.csv",
    nrows=100
)
```

Useful when exploring very large datasets.

---

## 5. skiprows

Skip unwanted rows.

```python
df = pd.read_csv(
    "employees.csv",
    skiprows=2
)
```

---

## 6. index_col

Specify the index column.

```python
df = pd.read_csv(
    "employees.csv",
    index_col="Employee_ID"
)
```

---

## 7. encoding

Specify file encoding.

```python
df = pd.read_csv(
    "employees.csv",
    encoding="utf-8"
)
```

Common encodings:

- utf-8
- latin1
- cp1252

---

## 8. sep

Specify a custom separator.

Comma-separated:

```python
pd.read_csv("employees.csv")
```

Pipe-separated:

```python
pd.read_csv(
    "employees.txt",
    sep="|"
)
```

---

## 9. na_values

Treat custom values as missing.

```python
df = pd.read_csv(
    "employees.csv",
    na_values=["NA", "-", "Missing"]
)
```

---

## 10. dtype

Specify column data types.

```python
df = pd.read_csv(
    "employees.csv",
    dtype={
        "Employee_ID": int,
        "Salary": float
    }
)
```

Improves consistency during data loading.

---

# 🏢 Industry Best Practices

- Always inspect the dataset after loading.
- Verify column names.
- Check data types.
- Validate missing values.
- Avoid loading unnecessary columns.
- Specify `dtype` when possible.
- Use `usecols` for large datasets.

---

# ❌ Common Mistakes

### Mistake 1

Wrong file path.

```python
pd.read_csv("employee.csv")
```

File does not exist.

---

### Mistake 2

Wrong separator.

CSV uses commas.

Using the wrong separator leads to incorrect parsing.

---

### Mistake 3

Ignoring encoding issues.

Some datasets require:

```python
encoding="latin1"
```

instead of UTF-8.

---

### Mistake 4

Loading unnecessary columns.

This wastes memory and increases processing time.

---

# 💼 Interview Questions

### Q1. What is a CSV file?

A CSV file is a plain text file where data is stored in rows and columns, separated by commas.

---

### Q2. Why is CSV widely used?

Because it is lightweight, portable, human-readable, and supported by most tools and programming languages.

---

### Q3. What does `read_csv()` return?

It returns a **Pandas DataFrame**.

---

### Q4. Why use `usecols`?

To load only the required columns, improving performance and reducing memory usage.

---

### Q5. Why specify `dtype` while reading data?

To ensure consistent data types and avoid incorrect type inference.

---

# 🧠 Engineer Thinking

When reading data, don't just think:

> "Can I load the file?"

Think:

- Is the file complete?
- Are the column names correct?
- Are the data types correct?
- Is the encoding correct?
- Do I need all the columns?
- Can I optimize memory usage?

This is how Machine Learning Engineers approach data loading.

---

# 📌 Summary

- CSV is the most common dataset format.
- Use `pd.read_csv()` to load CSV files.
- Learn important parameters like `usecols`, `dtype`, `encoding`, and `nrows`.
- Validate the dataset immediately after loading.
- Follow industry best practices for performance and reliability.

---

# 🚀 What's Next?

The next topic is:

**02-Excel.md**

You'll learn how to read Excel files using Pandas, work with multiple sheets, select specific worksheets, and handle Excel-specific options commonly used in industry.