# 📋 EDA Workflow & Checklist

> Exploratory Data Analysis is not a random collection of charts and commands. It is a highly structured, systematic process. This document provides the exact step-by-step workflow used by Senior Data Scientists.

---

# 📖 Table of Contents

1. Introduction
2. Learning Objectives
3. What is the EDA Workflow?
4. Why Do We Need a Strict Workflow?
5. Phase 1: Structural Discovery
6. Phase 2: Univariate Analysis (One by One)
7. Phase 3: Bivariate & Multivariate Analysis (Relationships)
8. Phase 4: Business Insight Extraction
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

- Follow a structured, repeatable EDA framework for any dataset.
- Transition logically from basic structural checks to complex statistical modeling.
- Document and present actionable business insights derived from EDA.

---

# 📘 What is the EDA Workflow?

The EDA Workflow is a sequential checklist that prevents you from jumping ahead. You cannot analyze relationships (Bivariate) until you understand the individual variables (Univariate), and you cannot understand variables until you understand the file structure.

---

# ❓ Why Do We Need a Strict Workflow?

Without a workflow, beginners load a dataset, plot a random scatter plot, generate a heatmap, and declare they are "done". They miss critical missing values, ignore skewness, and fail to understand the business context. A strict workflow guarantees nothing is missed.

---

# 📝 Phase 1: Structural Discovery

*Goal: Does the dataset load properly, and what are its dimensions?*

1. **Load Data**: `df = pd.read_csv()`
2. **Preview**: `df.head()` and `df.tail()` (Is there garbage at the bottom?)
3. **Dimensions**: `df.shape` (Is it 100 rows or 10 Million rows?)
4. **Data Types**: `df.info()` and `df.dtypes` (Are dates strings? Are numbers objects?)
5. **Missing Values**: `df.isnull().sum()` (Which columns are heavily corrupted?)
6. **Duplicates**: `df.duplicated().sum()` (Are there massive repeats?)

---

# 📊 Phase 2: Univariate Analysis

*Goal: Understand every single column in isolation.*

**For Numeric Columns:**
1. **Stats**: `df.describe()` (Check Min/Max for impossibilities).
2. **Shape**: Plot a Histogram/KDE (Is it Normal, Skewed, or Bimodal?).
3. **Outliers**: Plot a Box Plot (Are there extreme dots outside the whiskers?).

**For Categorical Columns:**
1. **Cardinality**: `df['Col'].nunique()` (Are there 2 categories or 5,000?).
2. **Imbalance**: `df['Col'].value_counts(normalize=True)` (Is 99% of the data "Yes"?).
3. **Visual**: Plot a `sns.countplot()`.

---

# 🔗 Phase 3: Bivariate & Multivariate Analysis

*Goal: How do the features interact with each other and the Target?*

1. **Target Isolation**: Identify your Target Variable (e.g., `Price`, `Churn`).
2. **Feature vs Target (Numeric)**: Scatter plots (Do they trend linearly?).
3. **Feature vs Target (Categorical)**: Box plots or Bar plots (Does category X have a higher mean than category Y?).
4. **Multicollinearity**: Generate a Correlation Heatmap (Are features highly correlated with *each other*?).
5. **Pair Plot**: Run `sns.pairplot()` on the top 5 most important features for a holistic overview.

---

# 💡 Phase 4: Business Insight Extraction

*Goal: Translate code into human language.*

1. **Group & Aggregate**: Use `groupby` to create Pivot Tables. (e.g., "The highest churn rate is in the 18-25 demographic in New York").
2. **Hypothesis Confirmation**: Did the data prove the business assumption?
3. **Documentation**: Write down 3 to 5 bullet points summarizing the most critical discoveries.

---

# 🏢 Real Industry Example

A Junior Data Scientist is handed a massive dataset on Customer Retention. 
Because they follow the EDA workflow strictly, they catch in **Phase 1** that 50% of the `Sign_Up_Date` column is missing. 
In **Phase 2**, they realize the `Age` column has a massive skew with a max of 999. 
In **Phase 3**, the Correlation Heatmap proves that `Usage_Frequency` is the only variable highly correlated with `Retention`. 
In **Phase 4**, they present a simple slide to the CEO stating: "Age data is corrupted, but if we increase Usage Frequency, retention skyrockets."

---

# 🧠 Engineer Thinking

During the workflow, constantly ask:

- **What am I looking for?** (Never plot a chart just to plot a chart. Plot it to answer a specific question).
- **Does this make sense?** (If the data shows that older people have lower incomes, does that align with real-world logic, or is the data mapped wrong?).

---

# ✅ Best Practices

- Use Jupyter Notebook Markdown cells extensively. Above every chart, write "Question: Does Age affect Price?". Below the chart, write "Conclusion: No, the scatter plot shows zero correlation."
- Save Phase 1 (Structural Discovery) as a reusable Python function, as you will run it on every dataset you ever touch.

---

# ❌ Common Mistakes

### Mistake 1
Skipping Phase 2 (Univariate) and jumping straight to Phase 3 (Heatmaps). A heatmap might show a 0.0 correlation, but if you skipped Univariate analysis, you wouldn't realize it's because the data was a Bimodal distribution or had massive outliers destroying the math.

---

# 💼 Interview Questions

### Q1. Walk me through your standard EDA process when you receive a new dataset.
*(Answer by citing the 4 phases: Structural checks, Univariate distribution checks, Bivariate correlation checks, and Business Insight extraction).*

### Q2. Why do we check Univariate statistics before Bivariate relationships?
You must ensure individual variables are clean, normally distributed, and free of extreme outliers before you can mathematically trust the relationship (correlation) between two variables.

---

# 📌 Summary

- EDA is a rigorous, 4-phase checklist.
- **Phase 1**: Structure & Cleanliness.
- **Phase 2**: Single Variables (Distributions/Outliers).
- **Phase 3**: Multiple Variables (Correlations/Trends).
- **Phase 4**: Business Translation.

---

# 🚀 Next Topic

The next topic is:

**15-Interview-Questions.md**

A comprehensive list of common Exploratory Data Analysis questions asked in Data Science and ML Engineering interviews to test everything you've learned in this module!
