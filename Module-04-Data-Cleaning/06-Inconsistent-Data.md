# 🧩 Inconsistent Data in Pandas

> Even after stripping whitespace and fixing capitalization, you will often find logically identical categories represented by different words. Resolving inconsistent data is vital for accurate categorical encoding.

---

# 📖 Table of Contents

1. Introduction
2. Learning Objectives
3. What is Inconsistent Data?
4. Why Do We Care?
5. Syntax & Methods
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

- Identify inconsistent categories using `value_counts()`.
- Use the `.replace()` method to map incorrect values to correct ones.
- Use `.map()` with a dictionary to standardize entire columns.

---

# 📘 What is Inconsistent Data?

Inconsistent data occurs when multiple distinct values represent the exact same real-world entity. 

Unlike dirty text (which has spaces or weird capitalization), inconsistent data involves completely different strings. For example: `"USA"`, `"United States"`, `"U.S.A."`, and `"America"` all refer to the same country.

---

# ❓ Why Do We Care?

If a dataset lists 5 variations of the United States, an ML algorithm will treat them as 5 completely distinct sovereign nations. 

If you build a model to predict house prices, and it learns that houses in `"USA"` are expensive, it will not apply that knowledge to houses located in `"America"`.

---

# 📝 Syntax & Methods

```python
# Method 1: Using replace (for specific value fixes)
df['Col'] = df['Col'].replace('Bad_Value', 'Good_Value')

# Method 2: Using replace with a dictionary
mapping = {'U.S.A.': 'USA', 'America': 'USA'}
df['Col'] = df['Col'].replace(mapping)

# Method 3: Using map (requires exhaustive mapping)
df['Col'] = df['Col'].map(mapping)
```

---

# ⚙️ Parameters

For `replace()`:

| Parameter | Description | Default |
|-----------|-------------|---------|
| `to_replace` | The value(s) you want to change. | Required |
| `value` | The new value. | Required |
| `inplace` | Modifies the DataFrame directly if True. | `False` |

---

# 💻 Example Dataset

```text
Employee_ID   Country
101           USA
102           United States
103           America
104           Canada
```

---

# 📌 Example 1 – Using replace() with a Dictionary

```python
import pandas as pd

df = pd.DataFrame({'Country': ['USA', 'United States', 'America', 'Canada']})

# Define a dictionary mapping bad values to the standard value
standardize_dict = {
    'United States': 'USA',
    'America': 'USA',
    'U.S.A.': 'USA'
}

df['Country'] = df['Country'].replace(standardize_dict)

print(df['Country'].values)
```

### Output
```text
['USA' 'USA' 'USA' 'Canada']
```
*Notice how 'Canada' was untouched because it wasn't in the dictionary!*

---

# 📌 Example 2 – Boolean Standardization

Often, Boolean values are recorded inconsistently by humans.

```python
df['Is_Active'] = ['Yes', 'Y', 'No', 'N']

bool_map = {
    'Yes': True, 'Y': True,
    'No': False, 'N': False
}

df['Is_Active'] = df['Is_Active'].replace(bool_map)
```

---

# 🏢 Real Industry Example

A Data Scientist working in Healthcare receives hospital records where the `Gender` column was entered as free-text. 

Running `df['Gender'].value_counts()` reveals:
- `M`: 500
- `Male`: 450
- `F`: 480
- `Female`: 420
- `man`: 10

The scientist creates a mapping dictionary `{'M': 'Male', 'man': 'Male', 'F': 'Female'}` and applies `.replace()` to unify the categories before training a diagnostic model.

---

# 🧠 Engineer Thinking

When standardizing data, ask yourself:

- Did I run `unique()` or `value_counts()` to see EVERY variation in the dataset before I built my mapping dictionary?
- Should I use `replace()` or `map()`? (`replace` leaves unmapped values alone. `map` turns unmapped values into `NaN`, which can accidentally destroy valid data).

---

# ⚡ Performance Notes

- Passing a dictionary to `.replace()` is highly optimized and much faster than using an `if/else` statement inside a `.apply()` function.

---

# ✅ Best Practices

- Always clean text (lower case, strip spaces) BEFORE dealing with inconsistent data. It drastically reduces the size of the dictionary you need to build.
- Store massive mapping dictionaries in separate JSON or YAML configuration files rather than hardcoding them in your Python script.

---

# ❌ Common Mistakes

### Mistake 1

Using `map()` when you only want to change a few values.

```python
df['Country'] = df['Country'].map({'America': 'USA'})
```
If you do this, 'Canada' becomes `NaN` because it wasn't defined in the dictionary! Always use `replace()` for partial mapping.

---

# 💼 Interview Questions

### Q1. How do you fix categorical columns that have multiple names for the same entity?
Create a mapping dictionary and use the `replace()` method.

---

### Q2. What is the difference between `replace()` and `map()` when passing a dictionary?
`replace()` updates only the keys provided and leaves the rest of the data intact. `map()` attempts to map every row; if a value is not in the dictionary, it turns it into a `NaN`.

---

# 📌 Summary

- Inconsistent data splits predictive power across redundant categories.
- Always check variations using `value_counts()`.
- Use mapping dictionaries combined with `.replace()` to unify categories securely.

---

# 🚀 Next Topic

The next topic is:

**07-Noise-Handling.md**

You'll learn how to deal with random variations in your data (like sensor jitter) by applying smoothing techniques.
