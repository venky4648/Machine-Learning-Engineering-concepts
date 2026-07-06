# 📊 Univariate Analysis

> Univariate means "One Variable". Univariate Analysis is the process of examining a single feature at a time through visual charts to understand its distribution, spread, and outliers.

---

# 📖 Table of Contents

1. Introduction
2. Learning Objectives
3. What is Univariate Analysis?
4. Why Do We Use It?
5. Key Visualizations (Histogram, Box Plot, Density)
6. Syntax (Seaborn & Matplotlib)
7. Examples
8. Output Interpretations
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

- Create Histograms to visualize data distributions.
- Create Density Plots (KDE) to see smooth distribution curves.
- Create Box Plots to visually detect extreme outliers.

---

# 📘 What is Univariate Analysis?

It is the simplest form of statistical analysis. The key objective is to describe the data and find patterns that exist within a *single column*, independent of any other column.

---

# ❓ Why Do We Use It?

While `df['Col'].skew()` gives you a number, a **Histogram** gives you a picture. Humans process shapes instantly. Univariate visual analysis confirms mathematical statistics (like skewness or IQR) with undeniable visual proof.

---

# 🖼️ Key Visualizations

1. **Histogram**: Chunks continuous numbers into "bins" (bars) to show frequency.
2. **Density Plot (KDE)**: A smoothed out version of a histogram (Kernel Density Estimation).
3. **Box Plot (Box-and-Whisker)**: A visual representation of the Interquartile Range (IQR). It explicitly plots outliers as isolated dots.

---

# 📝 Syntax

We use `seaborn` (built on top of `matplotlib`) because it requires significantly less code for beautiful charts.

```python
import seaborn as sns
import matplotlib.pyplot as plt

# Histogram & Density
sns.histplot(data=df, x='Numeric_Col', kde=True, bins=30)
plt.show()

# Box Plot
sns.boxplot(data=df, x='Numeric_Col')
plt.show()
```

---

# 💻 Example Dataset

Imagine a dataset of 1,000 employee `Salaries`. Most make around $60k, a few make $150k, and the CEO makes $2M.

---

# 📌 Example 1 – The Histogram & KDE

```python
import seaborn as sns
import matplotlib.pyplot as plt

# Creates a histogram with a smooth density line (kde=True)
sns.histplot(df['Salary'], bins=20, kde=True)
plt.title("Distribution of Salaries")
plt.xlabel("Salary ($)")
plt.show()
```

**Interpretation**: You will see a massive peak (bar) on the left side (around $60k), and a very long, flat tail dragging all the way to the right side where the CEO's $2M sits. This visually proves severe **Right Skew**.

---

# 📌 Example 2 – The Box Plot

```python
sns.boxplot(x=df['Salary'])
plt.title("Box Plot of Salaries")
plt.show()
```

**Interpretation**: 
- The colored "box" represents the middle 50% of people (IQR).
- The line inside the box is the Median.
- The "whiskers" extend to the acceptable bounds (1.5 * IQR).
- The CEO's $2M salary will be plotted as a literal dot far, far to the right of the whiskers, definitively proving it is a mathematical outlier.

---

# 🏢 Real Industry Example

A Data Scientist working at Airbnb plots a Histogram of `Nightly_Price`. They expect a bell curve. Instead, the histogram shows massive gaps, with huge spikes exactly at $99, $149, and $199. 

Univariate visual analysis revealed a psychological pricing phenomenon (hosts love ending prices in '9') that statistical summaries like `.mean()` completely missed.

---

# 🧠 Engineer Thinking

When looking at a Univariate plot, ask yourself:

- (Histogram): Is this a normal bell curve, or is it skewed? Are there two peaks (bimodal)?
- (Box Plot): Are there dots beyond the whiskers? Are there so many dots that it looks like a solid black line? If so, my data is completely warped by outliers.

---

# ⚡ Performance Notes

- Rendering visual plots on massive datasets (10M+ rows) takes time and crashes notebook UI. Always use `df.sample(100000)` to plot a representative sample instead.

---

# ✅ Best Practices

- Always experiment with the `bins=` parameter in Histograms. Too few bins hide the shape; too many bins make it look like random noise.
- Always add a Title and Labels. A chart without labels is useless to a business stakeholder.

---

# ❌ Common Mistakes

### Mistake 1
Plotting a Box Plot for Categorical Data.
Box plots rely on quartiles, medians, and numeric IQR. You cannot make a box plot of `City`. For categorical univariate analysis, use a standard Bar Chart (`sns.countplot()`).

---

# 💼 Interview Questions

### Q1. What does the "box" in a Box Plot represent?
It represents the Interquartile Range (IQR), which contains exactly the middle 50% of the data (from the 25th percentile to the 75th percentile).

### Q2. What is KDE in seaborn?
Kernel Density Estimation. It mathematically smooths out a histogram to show a continuous probability density curve.

---

# 📌 Summary

- Univariate Analysis looks at one column at a time.
- Histograms / KDEs are the standard for viewing Distribution and Skewness.
- Box Plots are the standard for visually detecting Outliers.

---

# 🚀 Next Topic

The next topic is:

**10-Bivariate-Analysis.md**

You will level up by analyzing *two* variables at the same time using Scatter Plots to visually prove correlations.
