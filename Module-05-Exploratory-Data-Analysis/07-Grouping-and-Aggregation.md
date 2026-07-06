# 🥞 Grouping and Aggregation

> `groupby()` is arguably the most powerful function in Pandas. It allows you to split your data into distinct groups, apply a calculation to each group, and combine the results into a beautiful summary table.

---

# 📖 Table of Contents

1. Introduction
2. Learning Objectives
3. What is Grouping & Aggregation?
4. Why Do We Use It?
5. Syntax (`groupby`, `agg`, `pivot_table`)
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

- Group data by categorical features using `groupby()`.
- Apply statistical functions (mean, sum, count) to groups.
- Perform multiple complex aggregations simultaneously using `agg()`.
- Create Excel-style cross-tabulations using `pivot_table()`.

---

# 📘 What is Grouping & Aggregation?

Grouping follows the **Split-Apply-Combine** paradigm:
1. **Split**: Break the dataset up based on a category (e.g., Department).
2. **Apply**: Run a math function on each chunk (e.g., Average Salary).
3. **Combine**: Put the results back into a single summary table.

---

# ❓ Why Do We Use It?

Global statistics are often misleading. If the global average salary is $70k, that doesn't tell you much. But if you group by Department and see that IT averages $100k while Sales averages $40k, you have uncovered a deep, actionable insight.

---

# 📝 Syntax

```python
# Simple GroupBy
df.groupby('Category_Col')['Numeric_Col'].mean()

# Multiple Aggregations using agg()
df.groupby('Category_Col').agg({
    'Numeric_Col1': 'mean',
    'Numeric_Col2': ['min', 'max', 'sum']
})

# Pivot Table
df.pivot_table(index='Category_Row', columns='Category_Col', values='Numeric_Col', aggfunc='mean')
```

---

# ⚙️ Parameters

For `agg()`:
Pass a dictionary where keys are column names and values are strings of functions (`'mean'`, `'sum'`, `'count'`).

For `pivot_table()`:

| Parameter | Description | Default |
|-----------|-------------|---------|
| `index` | The categorical column to use as rows. | Required |
| `columns` | The categorical column to use as columns. | None |
| `values` | The numeric column to calculate. | None |
| `aggfunc` | The math function to apply. | `'mean'` |

---

# 💻 Example Dataset

```text
Dept    City    Salary
IT      NY      100000
IT      LA      110000
HR      NY      60000
HR      LA      65000
```

---

# 📌 Example 1 – Simple GroupBy

```python
import pandas as pd

df = pd.DataFrame({
    'Dept': ['IT', 'IT', 'HR', 'HR'],
    'City': ['NY', 'LA', 'NY', 'LA'],
    'Salary': [100000, 110000, 60000, 65000]
})

# Average salary per department
print(df.groupby('Dept')['Salary'].mean())
```

### Output
```text
Dept
HR     62500.0
IT    105000.0
Name: Salary, dtype: float64
```

---

# 📌 Example 2 – Multiple Aggregations

```python
# Get the Min, Max, and Average salary per Dept
print(df.groupby('Dept')['Salary'].agg(['min', 'max', 'mean']))
```

### Output
```text
        min     max      mean
Dept                         
HR    60000   65000   62500.0
IT   100000  110000  105000.0
```

---

# 📌 Example 3 – Excel-Style Pivot Table

```python
# Create a matrix of Dept (rows) vs City (columns) showing average Salary
pt = df.pivot_table(index='Dept', columns='City', values='Salary', aggfunc='mean')
print(pt)
```

### Output
```text
City      LA      NY
Dept                
HR     65000   60000
IT    110000  100000
```

---

# 🏢 Real Industry Example

A Retail Data Analyst wants to find the best performing store regions. 

They use `groupby('Region')['Revenue'].sum().sort_values(ascending=False)` to instantly generate a ranked list of regions by total sales. They then use `agg()` to also pull the `count` of transactions, realizing that Region A has the most revenue, but Region B has way more foot traffic (transactions).

---

# 🧠 Engineer Thinking

When aggregating, ask yourself:

- Did `groupby` turn my category into the new Index? (Usually yes. Use `.reset_index()` afterward to flatten the DataFrame back to normal).
- Are there missing categories? `groupby` automatically drops `NaN` keys by default.

---

# ⚡ Performance Notes

- `groupby` is incredibly fast, but if you have dozens of columns, do not run `df.groupby('Col').mean()`. This forces Pandas to calculate the mean for every single numeric column. Always slice the exact column you want: `df.groupby('Col')['Target'].mean()`.

---

# ✅ Best Practices

- Always chain `.reset_index()` after a complex groupby if you plan to feed the resulting DataFrame into a machine learning model or a plotting library like Seaborn.
- Use `pivot_table()` when presenting findings to Business Stakeholders, as they are very comfortable reading Excel-style matrices.

---

# ❌ Common Mistakes

### Mistake 1
Not specifying a target column.

```python
# Bad: Calculates mean for EVERY numeric column in the dataset
df.groupby('Dept').mean() 

# Good: Only calculates mean for Salary
df.groupby('Dept')['Salary'].mean() 
```

---

# 💼 Interview Questions

### Q1. What is the difference between `groupby` and `pivot_table`?
`groupby` outputs a 1-dimensional Series (or MultiIndex DataFrame), which is great for code. `pivot_table` outputs a 2-dimensional grid (matrix), which is great for human readability and visualization.

### Q2. How do you apply different functions to different columns simultaneously?
By passing a dictionary to `.agg()`. (e.g., `df.agg({'Age': 'mean', 'Salary': 'sum'})`).

---

# 📌 Summary

- `groupby()` follows the Split-Apply-Combine logic.
- Use `.agg()` for advanced, multi-metric summaries.
- Use `pivot_table()` to generate 2D cross-tabulations.
- Grouping reveals local truths hidden by global averages.

---

# 🚀 Next Topic

The next topic is:

**08-Correlation-Analysis.md**

You'll mathematically prove whether two numerical features are related to each other (e.g., Does a larger house size strictly guarantee a higher price?).
