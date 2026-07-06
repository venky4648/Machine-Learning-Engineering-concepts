# 🧮 Statistical Summary

> A Statistical Summary moves your analysis from visually inspecting rows to mathematically understanding the dataset's central tendencies and spread.

---

# 📖 Table of Contents

1. Introduction
2. Learning Objectives
3. What is a Statistical Summary?
4. Why Do We Use It?
5. Syntax (`describe`, `mean`, `median`, `std`, etc.)
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

- Generate an all-in-one summary using `describe()`.
- Calculate central tendencies (`mean`, `median`, `mode`).
- Calculate dispersions (`std`, `var`, `min`, `max`, `quantile`).

---

# 📘 What is a Statistical Summary?

A statistical summary provides the descriptive statistics of your dataset. It mathematically summarizes large arrays of numbers into single metrics that define the data's center, shape, and variance.

---

# ❓ Why Do We Use It?

You cannot look at a column of 100,000 prices and understand it. But if you calculate that the `mean` is $50, the `min` is $10, and the `max` is $1,000,000, you instantly know the data is highly right-skewed and contains extreme outliers.

---

# 📝 Syntax

```python
# The Master Function
df.describe()

# Central Tendency
df['Col'].mean()
df['Col'].median()
df['Col'].mode()

# Spread / Dispersion
df['Col'].min()
df['Col'].max()
df['Col'].std()       # Standard Deviation
df['Col'].var()       # Variance
df['Col'].quantile(q) # Percentiles
```

---

# ⚙️ Parameters

| Function | Parameter | Description | Default |
|----------|-----------|-------------|---------|
| `describe` | `include` | Data types to include (e.g., `'all'`, `[np.number]`). | Numeric only |
| `quantile` | `q` | The percentile to compute (0.0 to 1.0). | `0.5` (Median) |

---

# 💻 Example Dataset

```text
Student   Score
1         85
2         90
3         85
4         95
5         1000  <-- Outlier
```

---

# 📌 Example 1 – The all-in-one `describe()`

```python
import pandas as pd

df = pd.DataFrame({'Score': [85, 90, 85, 95, 1000]})

print(df.describe())
```
This instantly outputs the count, mean, std, min, 25%, 50%, 75%, and max.

---

# 📌 Example 2 – Central Tendency

```python
print("Mean:", df['Score'].mean())     # Average
print("Median:", df['Score'].median()) # Middle value (50th percentile)
print("Mode:", df['Score'].mode()[0])  # Most frequent value
```
*(Notice how the Mean will be massively inflated by the score of 1000, but the Median remains unaffected).*

---

# 📌 Example 3 – Spread and Dispersion

```python
print("Standard Deviation:", df['Score'].std())
print("Variance:", df['Score'].var())
print("99th Percentile:", df['Score'].quantile(0.99))
```

---

# 🏢 Real Industry Example

A Quantitative Analyst evaluates algorithmic trading returns. They calculate the `mean()` return to see average profitability. However, they care much more about risk. They calculate the `std()` (Standard Deviation) of the returns. A high standard deviation indicates high volatility and massive risk, prompting them to adjust the algorithm.

---

# 🧠 Engineer Thinking

When reviewing these statistics, ask yourself:

- Is the `mean` drastically different from the `median`? If so, the data is skewed by outliers.
- Is the `min` value logically possible? (e.g., Negative values for human height).
- Is the `std` zero? (If standard deviation is 0, every value in the column is identical, meaning the column provides no predictive value to an ML model).

---

# ⚡ Performance Notes

- These vectorized Pandas operations are highly optimized. However, computing `mode()` can be slightly slower on massive textual datasets as it requires counting frequencies.

---

# ✅ Best Practices

- Always rely on `median()` rather than `mean()` for summarizing financial data (like Income or Home Prices) due to extreme outliers.
- Use `quantile(0.99)` and `quantile(0.01)` to find boundaries for capping outliers.

---

# ❌ Common Mistakes

### Mistake 1
Using `.mean()` on heavily skewed data. Averages lie when billionaires are in the room.

### Mistake 2
Forgetting that `describe()` ignores categorical (string) columns by default. You must use `describe(include='all')`.

---

# 💼 Interview Questions

### Q1. What is the difference between Standard Deviation and Variance?
Standard Deviation is the square root of Variance. It is preferred because it is expressed in the same units as the original data.

### Q2. Why is Median robust to outliers but Mean is not?
The Median is calculated strictly by positional rank, so extreme numerical values at the edges do not pull the center point.

---

# 📌 Summary

- `describe()` is the ultimate EDA starting point for numerical analysis.
- Central Tendency measures the "middle" (`mean`, `median`, `mode`).
- Dispersion measures the "spread" (`std`, `var`, `min`, `max`, `quantile`).

---

# 🚀 Next Topic

The next topic is:

**04-Data-Type-Analysis.md**

You'll explore how to deeply inspect and select features based on their specific data types using `info()` and `select_dtypes()`.
