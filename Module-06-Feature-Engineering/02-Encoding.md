# 🔠 Categorical Encoding

> Machine Learning models are purely mathematical equations. They cannot multiply or subtract words like "Red" or "Blue". Encoding is the mandatory process of converting categorical text into numbers.

---

# 📖 Table of Contents

1. Introduction
2. Learning Objectives
3. What is Encoding?
4. Why Do We Use It?
5. Techniques (Label vs One-Hot)
6. Syntax (Pandas & Scikit-Learn)
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

- Apply Label Encoding to ordinal data.
- Apply One-Hot Encoding to nominal data using Pandas `get_dummies()`.
- Avoid the "Dummy Variable Trap".

---

# 📘 What is Encoding?

Encoding replaces categorical strings (e.g., `City: "New York"`) with numerical values (e.g., `City: 1` or `City_NY: 1, City_LA: 0`).

---

# ❓ Why Do We Use It?

If you pass a column containing the word "Yes" into Scikit-Learn's Linear Regression or Random Forest, it will immediately crash with a `ValueError: could not convert string to float`. Every single column passed to an ML model must be a number.

---

# 🛠️ Two Primary Techniques

1. **Label Encoding (Ordinal)**: Replaces categories with ascending integers (0, 1, 2). Used when the data has an inherent order or ranking (e.g., Small, Medium, Large).
2. **One-Hot Encoding (Nominal)**: Creates a new binary column (0 or 1) for every unique category. Used when there is no order (e.g., Red, Green, Blue).

---

# 📝 Syntax

```python
import pandas as pd
from sklearn.preprocessing import LabelEncoder

# One-Hot Encoding (Pandas)
df = pd.get_dummies(df, columns=['Nominal_Col'], drop_first=True)

# Label Encoding (Scikit-Learn)
encoder = LabelEncoder()
df['Ordinal_Col'] = encoder.fit_transform(df['Ordinal_Col'])
```

---

# 💻 Example Dataset

```text
User   Size     City
1      Small    NY
2      Large    LA
3      Medium   NY
```

---

# 📌 Example 1 – Label Encoding (Ordinal Data)

`Size` has an order (Small < Medium < Large). We encode it with integers.

```python
import pandas as pd

df = pd.DataFrame({'Size': ['Small', 'Large', 'Medium']})

# Manual Mapping is often better for Ordinal to guarantee order
size_map = {'Small': 0, 'Medium': 1, 'Large': 2}
df['Size_Encoded'] = df['Size'].map(size_map)

print(df)
```
### Output
```text
     Size  Size_Encoded
0   Small             0
1   Large             2
2  Medium             1
```

---

# 📌 Example 2 – One-Hot Encoding (Nominal Data)

`City` has no mathematical order (NY is not "greater than" LA). If we Label Encoded it (NY=1, LA=2, CHI=3), the model would think CHI is 3 times larger than NY. We MUST use One-Hot Encoding.

```python
df = pd.DataFrame({'City': ['NY', 'LA', 'CHI']})

# One-Hot Encode (creating Dummy variables)
df_encoded = pd.get_dummies(df, columns=['City'], drop_first=True)

print(df_encoded)
```
### Output
```text
   City_LA  City_NY
0        0        1
1        1        0
2        0        0
```
*(Notice CHI is dropped due to `drop_first=True`. If LA=0 and NY=0, the model mathematically knows it must be CHI. This prevents Multicollinearity).*

---

# 🏢 Real Industry Example

An engineer is predicting car prices. The dataset has a `Make` column (Toyota, Ford, BMW, etc.) with 50 unique brands.

They apply `pd.get_dummies()`, turning 1 column into 49 new columns. The linear regression model is now able to assign a specific weight (price premium) to each individual car brand independently.

---

# 🧠 Engineer Thinking

When choosing an encoding strategy, ask yourself:

- Does this category have a ranking? (e.g., `Education_Level`: High School, Bachelors, Masters -> Use Label Encoding).
- Is this just a name or label with no rank? (e.g., `Color`, `City`, `Department` -> Use One-Hot Encoding).
- Are there 1,000 unique cities? (One-Hot Encoding will create 1,000 columns, causing the "Curse of Dimensionality". I should use Target Encoding instead).

---

# ⚡ Performance Notes

- `pd.get_dummies` is great for EDA, but in production pipelines, engineers use `sklearn.preprocessing.OneHotEncoder` because it can remember the categories and apply them consistently to future Test data.

---

# ✅ Best Practices

- Always use `drop_first=True` when One-Hot Encoding for Linear Models to avoid the Dummy Variable Trap (perfect multicollinearity).
- Tree-based models (Random Forest, XGBoost) do not require `drop_first=True`.

---

# ❌ Common Mistakes

### Mistake 1
Using Label Encoding on nominal data (like `Country`). 
If USA = 1, UK = 2, and Japan = 3, the algorithm will mathematically assume that `USA + UK = Japan`. This ruins the model.

---

# 💼 Interview Questions

### Q1. What is the Dummy Variable Trap?
It is a scenario in One-Hot Encoding where the newly created columns are perfectly correlated with each other. If you have Male=1 and Female=0, you don't need a Female column. Keeping both causes multicollinearity in linear models. We fix it by dropping one column (`drop_first=True`).

### Q2. When would you use Label Encoding over One-Hot Encoding?
When the categorical variable has an intrinsic order or hierarchy (Ordinal data), such as rating scales (Poor, Fair, Good, Excellent).

---

# 📌 Summary

- ML models only accept numbers.
- **Label Encoding**: Assigns integers (0, 1, 2) for ordered data.
- **One-Hot Encoding**: Creates binary (0/1) columns for unordered data.
- Always watch out for the Dummy Variable Trap in Linear algorithms.

---

# 🚀 Next Topic

The next topic is:

**03-Scaling.md**

You've turned words into numbers. Now, you will learn why the size of those numbers matters, and how to scale them to prevent algorithms from prioritizing large values over small values.
