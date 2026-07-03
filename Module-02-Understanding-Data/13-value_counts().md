# 📊 value_counts() in Pandas

> `value_counts()` is one of the most powerful EDA tools in Pandas. While `unique()` tells you the categories, and `nunique()` tells you how many there are, `value_counts()` tells you the exact distribution and frequency of each category.

---

# 📖 Table of Contents

1. Introduction
2. Learning Objectives
3. What is `value_counts()`?
4. Why Do We Use `value_counts()`?
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

- Calculate the frequency distribution of categorical data.
- Identify Class Imbalance in target variables.
- Convert counts into percentages (relative frequencies).
- Bin continuous numerical data into discrete intervals.

---

# 📘 What is `value_counts()`?

The `value_counts()` function returns a Series containing counts of unique values.

The resulting object is automatically sorted in descending order so that the most frequently occurring element is at the top.

---

# ❓ Why Do We Use `value_counts()`?

It is strictly required for understanding **Class Imbalance**.

If you are training a model to predict Cancer (Yes/No), and your dataset has 99,000 'No' and 1,000 'Yes', the model will simply guess 'No' every time and achieve 99% accuracy while being completely useless.

`value_counts()` instantly exposes these distributional imbalances so you know to apply techniques like SMOTE or class weighting.

---

# 📝 Syntax

```python
Series.value_counts(
    normalize=False,
    sort=True,
    ascending=False,
    bins=None,
    dropna=True
)
```

---

# ⚙️ Parameters

| Parameter | Description | Default |
|-----------|-------------|---------|
| `normalize` | Returns proportions/percentages instead of raw counts. | `False` |
| `sort` | Sorts the output by frequencies. | `True` |
| `ascending` | Sorts in ascending order (lowest frequency first). | `False` |
| `bins` | Groups continuous numeric data into half-open bins. | `None` |
| `dropna` | Excludes counts of missing values (`NaN`). | `True` |

---

# 💻 Example Dataset

```text
Employee_ID   Department
101           IT
102           HR
103           IT
104           IT
105           Sales
```

---

# 📌 Example 1 – Default Behavior

```python
import pandas as pd

df = pd.read_csv("employees.csv")

print(df['Department'].value_counts())
```

### Output

```text
IT       3
HR       1
Sales    1
Name: Department, dtype: int64
```
It is sorted with the most frequent department at the top.

---

# 📌 Example 2 – Getting Percentages

To see the distribution as percentages, use `normalize=True`.

```python
print(df['Department'].value_counts(normalize=True) * 100)
```

### Output

```text
IT       60.0
HR       20.0
Sales    20.0
Name: Department, dtype: float64
```
*60% of the employees belong to the IT department.*

---

# 📌 Example 3 – Binning Continuous Data

You can apply `value_counts()` to numeric columns by placing the numbers into bins.

```python
# Group ages into 3 bins
print(df['Age'].value_counts(bins=3))
```
This acts like a quick, text-based histogram.

---

# 🏢 Real Industry Example

A Data Scientist loads credit card fraud data. 

```python
df['Is_Fraud'].value_counts(normalize=True)
```
Output:
```text
False    0.998
True     0.002
```
They immediately see that fraud occurs in only 0.2% of transactions. They document severe class imbalance and pivot their strategy to use anomaly detection algorithms rather than standard logistic regression.

---

# 🧠 Engineer Thinking

When reviewing `value_counts()`, ask yourself:

- Is my target variable heavily imbalanced?
- Are there categories with only 1 or 2 occurrences? (These rare categories often act as noise and can be grouped into an "Other" category).
- Should I include `dropna=False` to see if a specific category is just masked by massive amounts of missing data?

---

# ⚡ Performance Notes

- Extremely fast for standard categorical series.
- Output is a Pandas Series, meaning you can immediately chain `.plot(kind='bar')` to visualize it.

---

# ✅ Best Practices

- Always run `value_counts(normalize=True)` on your target variable (`y`) before splitting your data.
- Combine rare classes. If a column has 50 categories but 45 of them make up less than 1% of the data, bundle them together.

---

# ❌ Common Mistakes

### Mistake 1

Forgetting that it drops `NaN` by default. 

If a column is 50% missing, `value_counts()` will make it look like the remaining 50% constitutes the entire dataset. Always use `dropna=False` during initial EDA.

---

# 💼 Interview Questions

### Q1. How do you find the percentage distribution of categorical variables?

By using `df['column'].value_counts(normalize=True)`.

---

### Q2. What is Class Imbalance and how do you detect it in Pandas?

Class imbalance occurs when one class completely dominates the others in the target variable. It is easily detected by running `value_counts()` on the target column.

---

### Q3. Can you use `value_counts()` on numeric data like Age or Income?

Yes, by using the `bins` parameter to group continuous data into discrete ranges.

---

# 📌 Summary

- `value_counts()` calculates frequency distributions.
- Use `normalize=True` for relative percentages.
- Use `bins` for grouping numeric data.
- Use `dropna=False` to expose missing values.
- Essential for detecting Class Imbalance.

---

# 🚀 Next Topic

Congratulations! You have completed **Module 02: Understanding Data**.

You now know how to preview datasets, check technical and statistical metadata, and analyze data types and distributions.

The next step in the roadmap is **Module 03: Data Validation**, where you will learn how to enforce rules and ensure data quality before beginning the cleaning process.
