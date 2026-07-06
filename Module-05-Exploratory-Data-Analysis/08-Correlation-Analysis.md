# 🔗 Correlation Analysis

> Correlation Analysis is the statistical engine behind Feature Selection. It proves mathematically whether two variables move together. If a feature has zero correlation with your target variable, it is useless to your model.

---

# 📖 Table of Contents

1. Introduction
2. Learning Objectives
3. What is Correlation?
4. Why Do We Use It?
5. Pearson Correlation Explained
6. Syntax (`corr`)
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

- Understand Pearson Correlation coefficients.
- Differentiate between Positive and Negative correlation.
- Generate a correlation matrix using `corr()`.
- Use Heatmaps to visually interpret correlation matrices.

---

# 📘 What is Correlation?

Correlation measures the strength and direction of the linear relationship between two continuous numerical variables.

- **Positive Correlation**: As X goes up, Y goes up (e.g., House Size & House Price).
- **Negative Correlation**: As X goes up, Y goes down (e.g., Car Weight & Fuel Efficiency).
- **No Correlation**: X and Y have no mathematical relationship.

---

# ❓ Why Do We Use It?

In Machine Learning, you want features that are highly correlated with your Target variable (Predictive Power). 
However, you DO NOT want features that are highly correlated with *each other* (Multicollinearity). If `House_Size_SqFt` and `House_Size_SqMeters` are perfectly correlated, feeding both to a model causes mathematical instability.

---

# 🧠 Pearson Correlation Explained

The standard metric is the **Pearson Correlation Coefficient (r)**:
- **+1.0**: Perfect Positive Correlation
- ** 0.0**: Zero Correlation (Random scatter)
- **-1.0**: Perfect Negative Correlation

*Rule of Thumb*: 
- |r| > 0.7 is Strong.
- |r| between 0.3 and 0.7 is Moderate.
- |r| < 0.3 is Weak.

---

# 📝 Syntax

```python
# Calculate correlation matrix for all numeric columns
corr_matrix = df.corr(method='pearson')

# Correlation of a single column against the rest
df.corr()['Target_Variable']
```

---

# 💻 Example Dataset

```text
Size_SqFt    Bedrooms    Age_Years    Price
1500         3           10           300k
2000         4           5            450k
1200         2           20           200k
```

---

# 📌 Example 1 – The Correlation Matrix

```python
import pandas as pd

df = pd.DataFrame({
    'Size': [1500, 2000, 1200, 2500],
    'Age': [10, 5, 20, 2],
    'Price': [300000, 450000, 200000, 600000]
})

print(df.corr())
```

### Output
```text
           Size       Age     Price
Size   1.000000 -0.963624  0.994689
Age   -0.963624  1.000000 -0.985184
Price  0.994689 -0.985184  1.000000
```
- The diagonal is always `1.0` (Size is perfectly correlated with Size).
- `Size` and `Price` have a **+0.99** (Strong Positive) correlation.
- `Age` and `Price` have a **-0.98** (Strong Negative) correlation (Older houses are cheaper).

---

# 📌 Example 2 – Visualizing with a Heatmap

Reading matrices with 50 columns is impossible. We use Seaborn Heatmaps.

```python
import seaborn as sns
import matplotlib.pyplot as plt

sns.heatmap(df.corr(), annot=True, cmap='coolwarm', vmin=-1, vmax=1)
plt.show()
```
*(Red indicates strong positive correlation, Blue indicates strong negative, and White indicates zero).*

---

# 🏢 Real Industry Example

A Data Scientist builds a model to predict Employee Attrition. They run a correlation matrix and find that `Distance_From_Home` has a +0.65 correlation with `Attrition` (longer commute = higher chance of quitting). 
However, they also notice that `Years_At_Company` and `Seniority_Level` have a +0.95 correlation with each other. To prevent Multicollinearity from destabilizing their Logistic Regression model, they drop `Seniority_Level`.

---

# 🧠 Engineer Thinking

When reviewing correlations, ask yourself:

- Did I accidentally include categorical (encoded) variables in a Pearson correlation? (Pearson only measures linear relationships between continuous numbers. It fails on categorical data).
- Are there two features with > 0.85 correlation? I should probably drop one of them.

---

# ⚡ Performance Notes

- `.corr()` compares every numerical column against every other numerical column. If you have 1,000 columns, this creates a 1,000 x 1,000 matrix, which is computationally expensive. 

---

# ✅ Best Practices

- Always plot a Heatmap. It makes communicating your findings to business stakeholders vastly easier.
- Use the `cmap='coolwarm'` or `cmap='RdYlGn'` palettes so red and green/blue naturally imply positive/negative ends of the spectrum.

---

# ❌ Common Mistakes

### Mistake 1
**Correlation equals Causation.**
Just because Ice Cream Sales and Shark Attacks have a +0.80 correlation does not mean ice cream causes shark attacks. They are both caused by a third variable (Summer Weather). Never assume causation based on `.corr()`.

### Mistake 2
Assuming a correlation of `0.0` means there is absolutely no relationship. Pearson ONLY measures *linear* (straight line) relationships. If the relationship is a perfect parabola (U-shape), Pearson will report `0.0`.

---

# 💼 Interview Questions

### Q1. What is Multicollinearity?
It is when two independent variables (features) are highly correlated with each other. This confuses linear models, making it impossible for the model to determine which feature is actually affecting the target.

### Q2. What does a Pearson coefficient of -0.9 indicate?
A very strong negative linear relationship. As X goes up, Y reliably goes down.

---

# 📌 Summary

- Correlation proves linear mathematical relationships.
- Use `.corr()` to generate the matrix.
- Use `sns.heatmap()` to visualize it.
- Keep features highly correlated with the target; drop features highly correlated with each other.

---

# 🚀 Next Topic

The next topic is:

**09-Univariate-Analysis.md**

You'll transition from looking at numbers in a console to generating powerful visual charts, starting with single-variable distributions like Histograms and Box Plots.
