# ℹ️ Using `info()` in Pandas

> Looking at the actual data values is great, but as an engineer, you need to understand the *schema* and the *health* of your dataset. `info()` provides a concise summary of the DataFrame's technical details.

---

# 📖 Table of Contents

1. What is `info()`?
2. Why Use `info()`?
3. Basic Usage and Output Analysis
4. Important Parameters
5. Industry Best Practices
6. Interview Questions
7. Summary

---

# 🎯 Learning Objectives

After completing this topic, you will be able to:
- Use `df.info()` to analyze DataFrame schema.
- Identify missing values quickly via Non-Null counts.
- Check data types to ensure numbers aren't stored as text.
- Monitor memory usage.

---

# 📘 What is `info()`?

The `info()` method prints information about a DataFrame, including:
- Total number of rows and index range.
- Total number of columns.
- Column names.
- Number of **non-null** values in each column.
- **Data type** (`dtype`) of each column.
- Memory usage.

---

# 🏢 Why Do Companies Use `info()`?

It is the fastest way to perform a "health check" on a dataset. 
- **Missing Data Detection**: If you have 10,000 rows, but a column has 8,000 non-null values, you immediately know 2,000 values are missing.
- **Type Checking**: If a `Salary` column shows up as `object` (text) instead of `float64` or `int64`, you know there is dirty data (like commas or dollar signs) breaking the column.

---

# 📂 Basic Usage

```python
import pandas as pd

df = pd.read_csv("employees.csv")

df.info()
```

**Example Output:**
```text
<class 'pandas.core.frame.DataFrame'>
RangeIndex: 1000 entries, 0 to 999
Data columns (total 4 columns):
 #   Column      Non-Null Count  Dtype  
---  ------      --------------  -----  
 0   Emp_ID      1000 non-null   int64  
 1   Name        980 non-null    object 
 2   Salary      1000 non-null   object 
 3   Join_Date   1000 non-null   object 
dtypes: int64(1), object(3)
memory usage: 31.4+ KB
```

### 🔍 Output Analysis:
1. **RangeIndex**: 1000 total rows (0 to 999).
2. **Name**: Only 980 non-nulls. We have 20 missing names.
3. **Salary**: Dtype is `object`. **Warning!** Salary should be a number. It likely contains `$50,000` text formatting.
4. **Join_Date**: Dtype is `object`. **Warning!** It should be `datetime64`.

---

# ⚙️ Important Parameters

## 1. `verbose`
For massive DataFrames with hundreds of columns, `info()` might truncate the output. Set `verbose=True` to force printing every column.
```python
df.info(verbose=True)
```

## 2. `show_counts`
If memory is low and dataset is huge, Pandas might skip counting non-nulls to save time. Set `show_counts=True` to force it.
```python
df.info(show_counts=True)
```

## 3. `memory_usage="deep"`
The default memory usage estimate is fast but inaccurate for string (`object`) columns. Use `"deep"` for the exact byte count.
```python
df.info(memory_usage="deep")
```

---

# ⚡ Industry Best Practices

✅ **Run `info()` before any cleaning**: It acts as your blueprint. Write down the anomalies (like wrong dtypes or missing counts) and create your data cleaning plan based on them.
✅ **Fix `object` types early**: In ML, models cannot process `object` strings natively. If a numeric feature shows as `object`, fix it immediately using string manipulation and `astype()`.

---

# 💼 Interview Questions

### Q1. What critical information does `df.info()` provide?
It provides the row count, column names, data types, non-null value counts, and memory usage.

### Q2. How can `df.info()` help identify missing data?
By comparing the total `RangeIndex` entries with the `Non-Null Count` of each column. Any column with a non-null count less than the total entries has missing data.

### Q3. Why might a numeric column show up as `object` in `info()`?
Because it contains non-numeric characters (like symbols, commas, or letters) or missing values represented as text (like "N/A"), forcing Pandas to treat the entire column as strings.

---

# 🧠 Engineer Thinking

When reviewing `info()`, ask yourself:
- Do the `dtypes` match the business reality of the feature? (Dates should be datetime, categories should be categorical, metrics should be float/int).
- Which columns require imputation for missing values based on the non-null counts?

---

# 📌 Summary

- `info()` is your primary diagnostic tool.
- It highlights missing values and data type mismatches.
- Use `memory_usage="deep"` for accurate memory sizing on large datasets.

---

# 🚀 What's Next?

The next topic is:

**[05-describe().md](05-describe().md)**

You will learn how to generate powerful statistical summaries for your data to identify outliers and distributions.
