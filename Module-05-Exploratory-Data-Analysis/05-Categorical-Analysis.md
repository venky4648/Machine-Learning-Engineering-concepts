# 🏷️ Categorical Analysis

> Categorical Analysis focuses on discrete, non-numerical groups (like Gender, Country, or Status). Understanding the cardinality and frequency of these groups is vital for encoding and detecting Class Imbalance.

---

# 📖 Table of Contents

1. Introduction
2. Learning Objectives
3. What is Categorical Analysis?
4. Why Do We Use It?
5. Syntax (`unique`, `nunique`, `value_counts`)
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

- Extract distinct categories using `unique()`.
- Measure feature cardinality using `nunique()`.
- Calculate frequency distributions and percentages using `value_counts()`.

---

# 📘 What is Categorical Analysis?

Categorical Analysis is the exploration of text or discrete variables. It answers questions like: "What are the possible values for this feature?", "How many unique values exist?", and "Which value is the most common?"

---

# ❓ Why Do We Use It?

You cannot feed words into an algorithm; you must encode them into numbers. 

Before doing so, you must verify the categories. If you have 500 distinct cities (`nunique`), One-Hot Encoding will create 500 new columns and crash your model. If one category appears 99% of the time (`value_counts`), you have massive class imbalance that needs fixing.

---

# 📝 Syntax

```python
# Returns an array of distinct values
df['Col'].unique()

# Returns the total count of distinct values (Cardinality)
df['Col'].nunique()

# Returns the frequency distribution (how many of each)
df['Col'].value_counts(normalize=False)
```

---

# ⚙️ Parameters

| Function | Parameter | Description | Default |
|----------|-----------|-------------|---------|
| `nunique` | `dropna` | Include `NaN` in the count if False. | `True` |
| `value_counts` | `normalize` | Return relative percentages instead of counts. | `False` |
| `value_counts` | `dropna` | Include `NaN` in the distribution. | `True` |

---

# 💻 Example Dataset

```text
User    Status
1       Active
2       Inactive
3       Active
4       Pending
5       Active
```

---

# 📌 Example 1 – Finding Distinct Values

```python
import pandas as pd

df = pd.DataFrame({'Status': ['Active', 'Inactive', 'Active', 'Pending', 'Active']})

print("Categories:", df['Status'].unique())
print("Cardinality:", df['Status'].nunique())
```

### Output
```text
Categories: ['Active' 'Inactive' 'Pending']
Cardinality: 3
```

---

# 📌 Example 2 – Frequency Distribution

```python
# Raw Counts
print(df['Status'].value_counts())

# Percentages
print(df['Status'].value_counts(normalize=True) * 100)
```

### Output (Percentages)
```text
Active      60.0
Inactive    20.0
Pending     20.0
Name: Status, dtype: float64
```

---

# 🏢 Real Industry Example

A Data Scientist building a Fraud Detection model runs `value_counts(normalize=True)` on the `Is_Fraud` target variable. 
It returns: `False: 99.9%, True: 0.1%`. 

They immediately realize the data is heavily imbalanced. If they don't apply techniques like SMOTE (Synthetic Minority Over-sampling Technique), their model will simply predict "False" every time and achieve 99.9% accuracy while catching zero actual fraud.

---

# 🧠 Engineer Thinking

When analyzing categories, ask yourself:

- Is the cardinality (`nunique`) too high for One-Hot Encoding? (If > 10, consider Target Encoding).
- Are there categories with only 1 or 2 occurrences in `value_counts()`? (Group them into an "Other" category to reduce noise).
- Do 'Yes' and 'yes' appear as two separate categories? (Clean the text!).

---

# ⚡ Performance Notes

- `value_counts()` is incredibly fast and automatically sorts results in descending order.

---

# ✅ Best Practices

- Always check `value_counts(dropna=False)` during initial EDA to ensure a massive chunk of missing data isn't hiding behind the visible categories.
- Drop columns where `nunique() == 1`, as zero-variance features provide no predictive power.

---

# ❌ Common Mistakes

### Mistake 1
Forgetting that `nunique()` and `value_counts()` drop `NaN` values by default, leading you to believe your dataset is 100% complete when it is not.

---

# 💼 Interview Questions

### Q1. What is Cardinality?
The number of distinct, unique values in a categorical column. High cardinality features require special encoding techniques.

### Q2. How do you find the percentage of occurrences for each category?
By passing `normalize=True` to the `value_counts()` function.

---

# 📌 Summary

- `unique()` extracts the actual categories.
- `nunique()` evaluates the cardinality.
- `value_counts()` exposes class imbalances and distributions.

---

# 🚀 Next Topic

The next topic is:

**06-Numerical-Analysis.md**

You'll explore numeric features in depth, analyzing their spread, central tendency, and the impact of outliers.
