# 🔄 Data Type Conversion in Pandas

> Even if your data looks perfectly clean to the human eye, if the underlying data type is wrong, your Machine Learning models will crash. Data Type Conversion ensures numbers act like numbers and dates act like dates.

---

# 📖 Table of Contents

1. Introduction
2. Learning Objectives
3. What is Data Type Conversion?
4. Why Do We Need It?
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

- Cast columns to different data types using `astype()`.
- Safely convert text to numeric values using `pd.to_numeric()`.
- Convert string dates into time-series objects using `pd.to_datetime()`.

---

# 📘 What is Data Type Conversion?

Data Type Conversion (or casting) is the process of changing a column's `dtype` from one format to another (e.g., from `object` (string) to `float64`).

---

# ❓ Why Do We Need It?

When Pandas reads a CSV file, it guesses the data types. If a single row in an `Age` column contains the word `"Unknown"`, Pandas will parse the entire column as an `object` (string). 

You cannot pass strings into mathematical algorithms like Linear Regression. You must convert that column back to a numeric type.

---

# 📝 Syntax

```python
# Method 1: astype() (Standard Casting)
df['Column'] = df['Column'].astype('type')

# Method 2: pd.to_numeric() (Safe casting for dirty numbers)
df['Column'] = pd.to_numeric(df['Column'], errors='coerce')

# Method 3: pd.to_datetime() (For Dates)
df['Column'] = pd.to_datetime(df['Column'])
```

---

# ⚙️ Parameters

For `pd.to_numeric()`:

| Parameter | Description | Default |
|-----------|-------------|---------|
| `errors` | What to do with un-convertible text. `'raise'` crashes, `'coerce'` turns them into `NaN`, `'ignore'` does nothing. | `'raise'` |

---

# 💻 Example Dataset

```text
Employee_ID   Age       Salary      Join_Date
101           25        $50000      2023-01-15
102           Unknown   $60000      2023-02-20
103           30        $70000      2023-03-01
```
*Note: `Age` contains text, `Salary` contains `$`, and `Join_Date` is just text.*

---

# 📌 Example 1 – Standard Casting with astype()

If a column is completely clean but just parsed incorrectly, you can use `.astype()`.

```python
import pandas as pd

# Suppose Employee_ID is read as float64, but we want it as a string
df['Employee_ID'] = df['Employee_ID'].astype(str)
```

*(Note: Never use `.astype(float)` if the column contains dirty text like `"Unknown"`, as it will instantly crash with a ValueError).*

---

# 📌 Example 2 – Safe Numeric Conversion

Because `Age` contains the word "Unknown", we use `pd.to_numeric` with `errors='coerce'`. This forcefully converts numbers, and turns un-convertible text into `NaN`.

```python
df['Age'] = pd.to_numeric(df['Age'], errors='coerce')

print(df['Age'])
```

### Output
```text
0    25.0
1     NaN   <-- "Unknown" safely became a Missing Value!
2    30.0
Name: Age, dtype: float64
```

---

# 📌 Example 3 – String Replacement + Casting

If a column has symbols (like `$50,000`), you must remove the symbols using string methods *before* casting to numeric.

```python
# Replace '$' with nothing, then cast to float
df['Salary'] = df['Salary'].str.replace('$', '').astype(float)
```

---

# 📌 Example 4 – Date Conversion

Strings cannot be used for time-series operations (like extracting the month).

```python
df['Join_Date'] = pd.to_datetime(df['Join_Date'])

# Now you can easily extract the month!
print(df['Join_Date'].dt.month)
```

---

# 🏢 Real Industry Example

An MLOps Engineer receives daily sales data. The `Revenue` column occasionally receives corrupted data like `"--"` instead of `0` due to a sensor glitch. 

Instead of building complex if-else logic, they simply write:
`df['Revenue'] = pd.to_numeric(df['Revenue'], errors='coerce').fillna(0)`

This single line elegantly forces the column to numeric, turns the glitches into `NaN`, and immediately fills those `NaN`s with `0`.

---

# 🧠 Engineer Thinking

When converting data, ask yourself:

- Did I accidentally turn valid data into `NaN` because I used `errors='coerce'` without cleaning the strings first? (e.g., coercing `"$500"` results in `NaN`. You must strip the `$` first).
- Should this numerical ID (like a Zip Code) actually be a string? (Yes, you never do math on Zip Codes, so they should be `object` or `category`).

---

# ⚡ Performance Notes

- `pd.to_datetime()` can be slow on massive datasets. Passing a specific `format` parameter (e.g., `format='%Y-%m-%d'`) drastically speeds up the conversion because Pandas doesn't have to guess the date layout for every row.

---

# ✅ Best Practices

- Always check `df.dtypes` after doing conversions to ensure they applied correctly.
- Convert low-cardinality text columns to `category` using `.astype('category')` to save massive amounts of RAM.

---

# ❌ Common Mistakes

### Mistake 1

Using `.astype(int)` on a column that has `NaN` values.

`NaN` is a float under the hood in NumPy. If you try to cast a column with NaNs to an integer, Pandas will throw an error. You must fill the NaNs first, or cast to `float64`.

---

# 💼 Interview Questions

### Q1. What happens if you use `pd.to_numeric` on a column with text and `errors='coerce'`?
Any string that cannot be mathematically converted into a number is replaced with `NaN`.

---

### Q2. How do you convert a string column representing dates into an actual datetime object?
By using `pd.to_datetime(df['column_name'])`.

---

### Q3. Why should ID columns (like Customer_ID or Zip_Code) be stored as strings/objects instead of integers?
Because they are categorical identifiers, not numerical values. Storing them as integers might tempt an ML model to mistakenly find mathematical relationships (e.g., assuming Zip Code 90210 is "greater" than Zip Code 10001).

---

# 📌 Summary

- Data must be the correct type before modeling.
- Use `.astype()` for clean, direct casting.
- Use `pd.to_numeric(errors='coerce')` to safely handle text mixed with numbers.
- Use `pd.to_datetime()` for time-series features.
- Clean text symbols (`$`, `,`) before attempting numeric conversion.

---

# 🚀 Next Topic

The next topic is:

**04-Outlier-Treatment.md**

You'll learn how to detect and handle extreme anomalies in your data that can drastically warp the accuracy of your models.
