# 🎤 EDA Interview Questions

> Exploratory Data Analysis is frequently tested in Data Science and Machine Learning interviews. Interviewers want to know if you can translate raw data into business value and if you know how to detect anomalies before building models.

---

# 📖 Table of Contents

1. Introduction
2. Conceptual Questions
3. Pandas & Syntax Questions
4. Statistical Questions
5. Scenario-Based Questions
6. Next Steps

---

# 🎯 Conceptual Questions

### Q1. What is the purpose of Exploratory Data Analysis?
**Answer:** The primary purpose of EDA is to help look at data before making any assumptions. It is used to identify errors, understand patterns, detect outliers and anomalous events, and find interesting relations among the variables. It prevents "Garbage In, Garbage Out".

### Q2. What is the difference between Univariate, Bivariate, and Multivariate Analysis?
**Answer:** 
- **Univariate:** Analyzing a single variable (e.g., Histogram of Ages) to understand its distribution and spread.
- **Bivariate:** Analyzing two variables simultaneously (e.g., Scatter plot of Age vs Salary) to determine empirical relationships.
- **Multivariate:** Analyzing more than two variables (e.g., Heatmap, or a Scatter plot with a color `hue`) to understand complex interactions and multicollinearity.

---

# 💻 Pandas & Syntax Questions

### Q3. How do you quickly get a high-level statistical overview of a DataFrame?
**Answer:** By using `df.describe()`. For categorical variables, you must use `df.describe(include='all')` or `df.describe(include=['O'])`.

### Q4. You need to apply a complex aggregation to different columns (e.g., Mean for Salary, Max for Age). How do you do this in Pandas?
**Answer:** By using `groupby()` chained with the `.agg()` method, passing a dictionary: `df.groupby('Department').agg({'Salary': 'mean', 'Age': 'max'})`.

### Q5. What is the difference between `df.isnull().sum()` and `df.info()`?
**Answer:** `df.info()` provides the count of *non-null* values, data types, and memory usage. `df.isnull().sum()` specifically returns the exact count of *missing* (null) values per column.

---

# 📈 Statistical Questions

### Q6. What does a Skewness value of 2.5 tell you about a feature?
**Answer:** It indicates a heavy right-skewed (positive skew) distribution. This means the mean is significantly greater than the median due to extreme outliers on the high end of the scale (e.g., income data).

### Q7. Explain the Interquartile Range (IQR) and how it is used to find outliers.
**Answer:** IQR is the difference between the 75th percentile (Q3) and the 25th percentile (Q1). It represents the middle 50% of the data. Outliers are typically defined mathematically as any value below `Q1 - 1.5 * IQR` or above `Q3 + 1.5 * IQR`.

### Q8. What is Multicollinearity, and why is it dangerous?
**Answer:** Multicollinearity occurs when two or more independent variables are highly correlated with each other (e.g., an r-value > 0.9 in a Pearson correlation matrix). It is dangerous for linear models because it makes it mathematically impossible for the model to determine the individual effect of each feature on the target variable.

---

# 🏢 Scenario-Based Questions

### Q9. You are handed a dataset with 50 numerical columns and 1 Target column. How do you decide which features to keep?
**Answer:** 
1. I would generate a Correlation Matrix and visualize it using a Seaborn Heatmap.
2. I would keep the features that have a high correlation (positive or negative) with the Target column.
3. I would check the features against *each other*. If Feature A and Feature B have a 0.95 correlation with each other, I will drop one of them to avoid multicollinearity.

### Q10. You plot a histogram of 'House Prices' and notice the data is heavily right-skewed. What do you do before feeding this to a Linear Regression model?
**Answer:** Linear Regression assumes normal distributions. I would apply a Logarithmic Transformation (`np.log1p()`) to the 'House Prices' column to compress the extreme outliers and pull the distribution closer to a normal bell curve.

### Q11. You are analyzing E-commerce transactions. A Box Plot reveals that a user purchased $5,000,000 worth of goods in one day. Do you delete this outlier?
**Answer:** No. An outlier should never be deleted blindly. I would investigate the context. If it's a data entry error, I might delete or impute it. However, in E-commerce, this could be a massive B2B wholesale transaction or extreme fraud. In either case, it holds massive business insight and should likely be kept or modeled separately.

---

# 🚀 Next Steps

Review these questions regularly. Being able to explain the *Why* behind EDA is much more important in an interview than remembering the exact Pandas syntax.

Move on to the **Resources.md** file for helpful cheat sheets!
