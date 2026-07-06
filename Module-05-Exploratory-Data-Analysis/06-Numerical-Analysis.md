# 🔢 Numerical Analysis

> Numerical Analysis dives deep into continuous and discrete numbers. It forms the mathematical backbone of your EDA, evaluating how numbers are distributed and identifying extreme values that break models.

---

# 📖 Table of Contents

1. Introduction
2. Learning Objectives
3. What is Numerical Analysis?
4. Why Do We Use It?
5. Key Concepts (Central Tendency, Spread, Outliers, Distribution)
6. Syntax
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

- Evaluate Central Tendency (Mean vs Median).
- Evaluate Spread (Variance, Standard Deviation).
- Analyze data Distributions (Normal vs Skewed).
- Statistically define and detect Outliers.

---

# 📘 What is Numerical Analysis?

Numerical Analysis is the mathematical evaluation of quantitative columns (e.g., Age, Income, Height, Price). It focuses heavily on four pillars:
1. **Central Tendency** (Where is the middle?)
2. **Spread/Dispersion** (How wide is the data?)
3. **Distribution** (What shape does the data make?)
4. **Outliers** (Are there extreme anomalies?)

---

# ❓ Why Do We Use It?

Machine Learning models make assumptions. Linear models assume Normal Distributions. Distance-based models (like K-Means) assume all features have a similar Spread (Variance). If you don't analyze these numbers and scale/transform them appropriately, your algorithms will fail.

---

# 🧠 Key Concepts

- **Distribution**: The shape of the data. A Normal Distribution looks like a symmetrical Bell Curve.
- **Spread**: If the standard deviation is small, the data points are clustered tightly around the mean. If it is large, the data is spread far apart.
- **Central Tendency**: The balancing point of the data.
- **Outliers**: Extreme values (usually defined as anything outside 1.5 * IQR or > 3 Standard Deviations).

---

# 📝 Syntax

We use the Pandas `.describe()` and NumPy functions covered in the Statistical Summary, combined with targeted checks:

```python
# Central Tendency
df['Col'].mean()
df['Col'].median()

# Spread
df['Col'].std()

# Distribution (Skewness)
df['Col'].skew()
```

---

# 💻 Example Dataset

```text
House_ID   Price ($)
1          200000
2          210000
3          195000
4          205000
5          5000000  <-- Mansion
```

---

# 📌 Example 1 – Central Tendency vs Spread

```python
import pandas as pd

df = pd.DataFrame({'Price': [200000, 210000, 195000, 205000, 5000000]})

print("Mean:", df['Price'].mean())
print("Median:", df['Price'].median())
print("Std Dev:", df['Price'].std())
```

### Output
```text
Mean: 1162000.0
Median: 205000.0
Std Dev: 2145715.5
```
Because of the $5M mansion (outlier), the Mean is highly distorted. The Median accurately reflects a typical house. The massive Std Dev confirms extreme variance.

---

# 📌 Example 2 – Distribution (Skewness)

```python
print("Skewness:", df['Price'].skew())
```

### Output
```text
Skewness: 2.23
```
A skewness > 1 indicates a heavy right tail. This tells the engineer a Log Transformation is required before applying Linear Regression.

---

# 🏢 Real Industry Example

An insurance company is setting premiums based on `Driver_Age`. 

A data analyst runs a numerical analysis and notices the `min()` age is -5 and the `max()` is 150. These are physically impossible outliers caused by data entry errors. The analyst removes these records. Then, they look at the Spread (Variance). Since driver risk heavily correlates with age variance, they bin the continuous ages into categorical groups ("18-25", "26-40", etc.) to stabilize the variance for the model.

---

# 🧠 Engineer Thinking

When analyzing numbers, ask yourself:

- Are the numbers on vastly different scales? (e.g., `Age` is 0-100, but `Salary` is 0-1,000,000). If so, I must apply Feature Scaling (Standardization/Normalization).
- Are there 0s where 0s shouldn't exist? (Often, systems use `0` to represent a missing value).

---

# ⚡ Performance Notes

- Avoid looping through numeric columns to calculate stats. Always use vectorized functions like `.describe()`, `.mean()`, and `.skew()`.

---

# ✅ Best Practices

- Always compare Mean to Median. If `Mean >> Median`, you have right skew. If `Mean << Median`, you have left skew.
- Visualize your numerical analysis immediately using Histograms and Box Plots (covered in upcoming sections).

---

# ❌ Common Mistakes

### Mistake 1
Treating ID columns (like `Zip_Code` or `Employee_ID`) as numbers. Just because it is a digit doesn't mean it holds mathematical value. You should never calculate the `mean()` of a Zip Code!

---

# 💼 Interview Questions

### Q1. How does a massive outlier affect the Mean and the Median?
A massive outlier pulls the Mean heavily in its direction, but leaves the Median largely unaffected, which is why the Median is preferred for skewed financial data.

### Q2. What does a Skewness value of 0 indicate?
It indicates a perfectly symmetrical distribution (a Normal Distribution / Bell Curve).

---

# 📌 Summary

- Numerical Analysis focuses on Central Tendency, Spread, Distribution, and Outliers.
- Skewness dictates if mathematical transformations are needed.
- High variance often dictates if Feature Scaling is required.

---

# 🚀 Next Topic

The next topic is:

**07-Grouping-and-Aggregation.md**

You'll learn how to break your data down by categories (e.g., average salary *by department*) using Pandas' most powerful tool: `groupby()`.
