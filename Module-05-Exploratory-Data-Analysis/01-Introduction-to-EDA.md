# 🧭 Introduction to EDA

> Exploratory Data Analysis (EDA) is the art of asking your data questions and using code and visuals to find the answers. It is the detective work of Data Science.

---

# 📖 Table of Contents

1. Introduction
2. Learning Objectives
3. What is EDA?
4. Why Do We Use EDA?
5. Syntax / Core Libraries
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

- Define what Exploratory Data Analysis is.
- Understand the core goals of EDA.
- Identify the standard Python libraries used for EDA.

---

# 📘 What is EDA?

Exploratory Data Analysis (EDA) is an approach to analyzing datasets to summarize their main characteristics, often with visual methods. 

It was promoted by statistician John Tukey to encourage statisticians to explore the data, formulate hypotheses, and understand the data's underlying structure before formally modeling it.

---

# ❓ Why Do We Use EDA?

We perform EDA to:
- Maximize insights into a dataset.
- Uncover underlying structure and hidden patterns.
- Extract important variables.
- Detect outliers and anomalies.
- Test underlying assumptions.

---

# 📝 Syntax / Core Libraries

EDA doesn't have a single "syntax". Instead, it relies on a stack of core Python libraries:

```python
import pandas as pd       # For data manipulation
import numpy as np        # For mathematical operations
import matplotlib.pyplot as plt  # For basic plotting
import seaborn as sns     # For advanced statistical plotting
```

---

# ⚙️ Parameters

Since EDA is an approach rather than a single function, the parameters depend entirely on the tool you are using (e.g., `bins` for a histogram, `hue` for a seaborn scatterplot).

---

# 💻 Example Dataset

During this module, we will explore datasets conceptually similar to real-world business data: e.g., Customer Churn data, Housing Prices, or E-Commerce Sales.

---

# 📌 Example 1 – The First Step of EDA

The first step of any EDA is always loading the data and asking basic questions.

```python
import pandas as pd

df = pd.read_csv('data.csv')

# What does the data look like?
print(df.head())
```

---

# 🏢 Real Industry Example

A team is tasked with building a model to predict Loan Defaults. 

Before writing a single line of Machine Learning code, the Lead Data Scientist spends three days doing EDA. During EDA, they plot a histogram of `Income` and realize that 5% of the data has an income of `$999,999,999`. 

Because of EDA, they realize this is a system error code for "Missing Income". If they had skipped EDA, the model would have assumed these people were billionaires!

---

# 🧠 Engineer Thinking

When starting EDA, ask yourself:

- What is the business problem we are trying to solve?
- What does each column represent in the real world?
- Are there logical relationships I expect to see? (e.g., Older houses should generally be cheaper unless they are historical).

---

# ⚡ Performance Notes

- Visualizing data with millions of rows can crash your notebook. Always use `.sample()` to plot a representative subset of massive datasets during EDA.

---

# ✅ Best Practices

- **Document your findings**: EDA is useless if you don't write down your insights. Use Markdown cells in Jupyter to record what you see.
- **Don't jump to conclusions**: Correlation does not equal causation.

---

# ❌ Common Mistakes

### Mistake 1

Skipping straight to Machine Learning. 

Beginners often load data and immediately type `model.fit()`. This is guaranteed to result in terrible models because the data was never understood or formatted correctly.

---

# 💼 Interview Questions

### Q1. What is the main goal of EDA?
To understand the underlying structure, detect anomalies, test assumptions, and find patterns before modeling.

### Q2. Who coined the term Exploratory Data Analysis?
John Tukey, an American mathematician and statistician.

---

# 📌 Summary

- EDA is the investigative phase of Data Science.
- It relies heavily on Pandas, Matplotlib, and Seaborn.
- It is a mandatory step before any Machine Learning occurs.

---

# 🚀 Next Topic

The next topic is:

**02-Dataset-Overview.md**

You'll dive into the specific Pandas functions used to get a high-level structural overview of your dataset.
