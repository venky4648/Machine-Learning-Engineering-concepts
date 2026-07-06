# 🏭 Data Cleaning Pipeline

> Cleaning data step-by-step in a Jupyter Notebook is fine for exploration, but in production, you must automate the process. A Data Cleaning Pipeline wraps all your rules into a single, reproducible function.

---

# 📖 Table of Contents

1. Introduction
2. Learning Objectives
3. What is a Pipeline?
4. Why Do We Need It?
5. The Architecture of a Cleaning Pipeline
6. Example Pipeline Code
7. Industry Example
8. Engineer Thinking
9. Best Practices
10. Common Mistakes
11. Interview Questions
12. Summary
13. Next Topic

---

# 🎯 Learning Objectives

After completing this topic, you will be able to:

- Transition from "Notebook code" to "Production code".
- Wrap multiple Pandas cleaning steps into a single Python function.
- Ensure the pipeline can be applied equally to Training data and Future data.

---

# 📘 What is a Pipeline?

A Data Cleaning Pipeline is a structured sequence of data processing steps. It takes raw, dirty data as input, automatically applies all validation, imputation, and transformation logic in order, and outputs clean data ready for modeling.

---

# ❓ Why Do We Need It?

When you deploy a Machine Learning model, it will receive new, unseen data every day. 

If you cleaned your training data by manually running 15 scattered cells in a Jupyter Notebook, you cannot replicate that process in production. A pipeline guarantees that **new data undergoes the exact same cleaning process as the training data**.

---

# 🏗️ The Architecture of a Cleaning Pipeline

A standard pipeline follows this exact order:

1. **Standardize Columns** (Lowercase, snake_case)
2. **Remove Duplicates**
3. **Correct Data Types** (pd.to_numeric, datetime)
4. **Clean Text/Categories** (strip, replace dictionaries)
5. **Handle Missing Values** (dropna, fillna)
6. **Treat Outliers** (capping)
7. **Transformations** (Log)

---

# 💻 Example Pipeline Code

Here is how you build a production-ready pipeline using a Python function.

```python
import pandas as pd
import numpy as np

def clean_data_pipeline(df):
    """
    Executes the standard data cleaning pipeline.
    """
    # 1. Standardize Columns
    df.columns = df.columns.str.strip().str.lower().str.replace(' ', '_')
    
    # 2. Remove Duplicates
    df = df.drop_duplicates()
    
    # 3. Data Types
    if 'join_date' in df.columns:
        df['join_date'] = pd.to_datetime(df['join_date'])
        
    # 4. Text Cleaning
    if 'city' in df.columns:
        df['city'] = df['city'].str.strip().str.title()
        
    # 5. Missing Values
    if 'salary' in df.columns:
        # Fill missing salary with median
        median_salary = df['salary'].median()
        df['salary'] = df['salary'].fillna(median_salary)
        
    # 6. Outlier Capping (Assume predefined upper bound)
    upper_bound = 150000
    df['salary'] = np.where(df['salary'] > upper_bound, upper_bound, df['salary'])
    
    return df
```

---

# 📌 Applying the Pipeline

```python
# Load Raw Data
raw_train_df = pd.read_csv("train.csv")
raw_test_df = pd.read_csv("test.csv")

# Apply Pipeline
clean_train_df = clean_data_pipeline(raw_train_df)
clean_test_df = clean_data_pipeline(raw_test_df)
```

By using a single function, we guarantee the exact same rules are applied to both datasets!

---

# 🏢 Real Industry Example

At a major tech company, Data Scientists do not write pipelines in standard Python functions. They use the `Pipeline` class from `scikit-learn` or custom transformers. 

This ensures that statistics (like the Median Salary for imputation) are calculated *only* on the Training data, and those exact same stored numbers are applied to the Test data, preventing Data Leakage.

*(Note: You will learn about Scikit-Learn Pipelines in Module 07).*

---

# 🧠 Engineer Thinking

When building a pipeline, ask yourself:

- Is the order of operations correct? (e.g., If you handle missing values before converting text to numeric, you might miss `NaN`s that were hidden as text strings).
- Did I hardcode any values? (e.g., Don't hardcode `upper_bound = 150000`, calculate it dynamically using IQR, or pass it as an argument).

---

# ✅ Best Practices

- Use `assert` statements inside your pipeline to validate data. `assert df.duplicated().sum() == 0` ensures duplicates were actually removed.
- Add logging. `print(f"Dropped {dropped_count} rows")` helps you monitor the pipeline when it runs in the cloud.

---

# ❌ Common Mistakes

### Mistake 1

Hardcoding column names without checking if they exist.

If tomorrow's dataset doesn't include the `city` column, your pipeline will throw a `KeyError` and crash the entire server. Always use `if 'column_name' in df.columns:` before cleaning it.

---

# 💼 Interview Questions

### Q1. Why is it bad practice to clean data step-by-step in a notebook without creating a pipeline?
Because it is not reproducible. You cannot deploy scattered notebook cells into a production server to clean incoming live data.

### Q2. What is the correct order of operations in a cleaning pipeline?
Generally: Standardize Columns -> Drop Duplicates -> Type Conversion -> Text Cleaning -> Missing Values -> Outliers -> Transformations.

---

# 📌 Summary

- A pipeline converts data cleaning from an ad-hoc task into a software engineering component.
- It ensures reproducibility between Training and Production data.
- Always check if columns exist before applying logic to avoid `KeyError` crashes.

---

# 🚀 Next Topic

Congratulations! You have completed **Module 04: Data Cleaning**.

You now have the skills to handle missing values, outilers, noisy text, and compile everything into a production-ready pipeline.

The next step in the roadmap is **Module 05: Exploratory Data Analysis (EDA)**, where you will learn how to visually and statistically uncover hidden patterns in your newly cleaned data.
