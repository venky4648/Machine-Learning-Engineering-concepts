# 📊 Reading Excel Files in Pandas

> Excel files are one of the most common data sources in business, finance, HR, healthcare, and analytics. As a Machine Learning Engineer, you will frequently receive datasets in Excel format. Learning how to efficiently read Excel files is an essential skill.

---

# 📖 Table of Contents

1. Introduction
2. What is an Excel File?
3. Why Do Companies Use Excel?
4. Installing Required Library
5. Reading Excel Files
6. Important Parameters
7. Working with Multiple Sheets
8. Industry Best Practices
9. Common Errors
10. Interview Questions
11. Summary

---

# 🎯 Learning Objectives

After completing this topic, you will be able to:

- Read Excel files using Pandas.
- Load specific worksheets.
- Read multiple worksheets.
- Select required columns.
- Optimize Excel loading.
- Handle common Excel issues.

---

# 📘 What is an Excel File?

Excel files are spreadsheet files created using Microsoft Excel.

Common extensions:

- `.xlsx` (Modern Excel format)
- `.xls` (Older Excel format)

Unlike CSV files, Excel files can contain:

- Multiple sheets
- Formatting
- Charts
- Formulas
- Tables

---

# 🏢 Why Do Companies Use Excel?

Excel is widely used because:

- Business users are familiar with it.
- Multiple sheets can store related information.
- Supports formulas and calculations.
- Easy reporting and visualization.
- Simple data sharing.

Typical departments using Excel:

- Human Resources
- Finance
- Sales
- Operations
- Marketing
- Inventory Management

---

# 📦 Install Required Library

Pandas uses **openpyxl** to read modern Excel files.

Install:

```bash
pip install openpyxl
```

---

# 📥 Import Pandas

```python
import pandas as pd
```

---

# 📂 Reading an Excel File

```python
import pandas as pd

df = pd.read_excel("employees.xlsx")
```

---

# 📊 Example Dataset

Sheet: Employees

| Employee_ID | Name | Age | Department | Salary |
|-------------|------|-----|------------|--------|
|101|Ram|25|IT|50000|
|102|Ravi|28|HR|60000|
|103|John|30|Finance|70000|

---

Python Code

```python
import pandas as pd

df = pd.read_excel("employees.xlsx")

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

## 1. sheet_name

Read a specific worksheet.

```python
df = pd.read_excel(
    "employees.xlsx",
    sheet_name="Employees"
)
```

You can also use the sheet index.

```python
df = pd.read_excel(
    "employees.xlsx",
    sheet_name=0
)
```

---

## 2. usecols

Read only required columns.

```python
df = pd.read_excel(
    "employees.xlsx",
    usecols=["Name", "Salary"]
)
```

Benefits:

- Faster loading
- Lower memory usage
- Better performance

---

## 3. nrows

Read only the first few rows.

```python
df = pd.read_excel(
    "employees.xlsx",
    nrows=100
)
```

Useful for previewing large files.

---

## 4. skiprows

Skip unnecessary rows.

```python
df = pd.read_excel(
    "employees.xlsx",
    skiprows=2
)
```

---

## 5. header

Specify which row contains column names.

```python
df = pd.read_excel(
    "employees.xlsx",
    header=1
)
```

---

## 6. names

Assign custom column names.

```python
columns = [
    "ID",
    "Name",
    "Age",
    "Department",
    "Salary"
]

df = pd.read_excel(
    "employees.xlsx",
    names=columns
)
```

---

## 7. index_col

Use a specific column as the DataFrame index.

```python
df = pd.read_excel(
    "employees.xlsx",
    index_col="Employee_ID"
)
```

---

## 8. dtype

Specify column data types.

```python
df = pd.read_excel(
    "employees.xlsx",
    dtype={
        "Employee_ID": int,
        "Salary": float
    }
)
```

---

# 📑 Reading Multiple Sheets

Suppose an Excel file contains:

- Employees
- Departments
- Salaries

Read all sheets.

```python
all_sheets = pd.read_excel(
    "company.xlsx",
    sheet_name=None
)
```

Output:

```python
{
    "Employees": DataFrame,
    "Departments": DataFrame,
    "Salaries": DataFrame
}
```

---

Read selected sheets.

```python
data = pd.read_excel(
    "company.xlsx",
    sheet_name=["Employees", "Departments"]
)
```

---

# 🏢 Real Industry Example

An HR department sends:

```
company_data.xlsx
```

Sheets:

- Employees
- Departments
- Attendance
- Leaves

As a Machine Learning Engineer, you may only need:

- Employees
- Attendance

Reading only the required sheets improves performance.

---

# ⚡ Performance Tips

✅ Read only required sheets.

✅ Use `usecols` to reduce memory.

✅ Avoid loading unnecessary data.

✅ Convert data types after loading if required.

---

# ❌ Common Mistakes

### Mistake 1

Forgetting to install `openpyxl`.

Result:

```text
ImportError: Missing optional dependency 'openpyxl'
```

---

### Mistake 2

Using the wrong sheet name.

```python
sheet_name="Employee"
```

When the actual sheet is:

```text
Employees
```

This raises an error.

---

### Mistake 3

Loading all sheets when only one is required.

This wastes memory and processing time.

---

### Mistake 4

Ignoring merged cells and formatting.

Pandas reads values, not Excel formatting.

---

# 💼 Interview Questions

### Q1. Which function reads Excel files in Pandas?

```python
pd.read_excel()
```

---

### Q2. Which library is required for reading `.xlsx` files?

```
openpyxl
```

---

### Q3. How do you read a specific worksheet?

```python
pd.read_excel(
    "employees.xlsx",
    sheet_name="Employees"
)
```

---

### Q4. How do you read every sheet in an Excel file?

```python
pd.read_excel(
    "company.xlsx",
    sheet_name=None
)
```

---

### Q5. Why use `usecols`?

To load only required columns, reducing memory usage and improving performance.

---

# 🧠 Engineer Thinking

When reading Excel files, ask yourself:

- Do I need every sheet?
- Do I need every column?
- Is the header row correct?
- Are data types correct?
- Is the file maintained manually (higher chance of inconsistencies)?
- Should I validate the data immediately after loading?

Excel files often come from manual business processes, so validation is especially important.

---

# 📌 CSV vs Excel

| Feature | CSV | Excel |
|---------|-----|-------|
| Multiple Sheets | ❌ No | ✅ Yes |
| Formatting | ❌ No | ✅ Yes |
| File Size | Smaller | Larger |
| Speed | Faster | Slightly Slower |
| Human Editing | Limited | Excellent |
| Charts & Formulas | ❌ No | ✅ Yes |

---

# 📌 Summary

- Use `pd.read_excel()` to load Excel files.
- Install `openpyxl` for `.xlsx` support.
- Use `sheet_name` to select worksheets.
- Use `usecols` and `nrows` for better performance.
- Validate data after loading because Excel files are often manually maintained.
- Read only the sheets and columns required for your analysis.

---

# 🚀 What's Next?

The next topic is:

**03-JSON.md**

You'll learn how to work with JSON data from APIs, nested structures, and web applications—a critical skill for modern Machine Learning and Data Engineering workflows.