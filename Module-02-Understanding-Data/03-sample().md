# 🎲 Using `sample()` in Pandas

> `head()` and `tail()` are great, but they only show the extremes. In sorted or chronologically ordered datasets, the beginning and end might look completely different from the middle. `sample()` solves this by grabbing random rows.

---

# 📖 Table of Contents

1. What is `sample()`?
2. Why Use `sample()`?
3. Basic Usage
4. Important Parameters
5. Industry Best Practices
6. Interview Questions
7. Summary

---

# 🎯 Learning Objectives

After completing this topic, you will be able to:
- Extract random subsets of data using `df.sample()`.
- Set random seeds for reproducibility.
- Sample fractions of a dataset instead of exact numbers.

---

# 📘 What is `sample()`?

The `sample()` method returns a random selection of rows (or columns) from the DataFrame. By default, it returns **1 random row**.

---

# 🏢 Why Do Companies Use `sample()`?

- **Unbiased Inspection**: If data is sorted by `Country`, `head()` might only show "Afghanistan" and `tail()` might only show "Zimbabwe". `sample()` lets you see a mix of countries.
- **Creating Mini-Datasets**: When building complex data pipelines or testing slow machine learning models, engineers use `sample()` to create a small, representative 1% dataset to test their code quickly before running it on the 100GB file.

---

# 📂 Basic Usage

```python
import pandas as pd

df = pd.read_csv("customers.csv")

# Return 1 random row
print(df.sample())

# Return 5 random rows
print(df.sample(5))
```

---

# ⚙️ Important Parameters

## 1. `n` (Number of rows)
Specify exactly how many random rows you want.
```python
df.sample(n=10)
```

## 2. `frac` (Fraction of the dataset)
Instead of a fixed number, return a percentage of the total rows.
```python
# Returns 10% of the dataset
df.sample(frac=0.1) 
```

## 3. `random_state` (Reproducibility)
If you run `sample()` multiple times, you get different rows. To get the *same* random rows every time (crucial for debugging or teaching), set a seed.
```python
df.sample(n=5, random_state=42)
```

## 4. `replace` (Sampling with replacement)
Allow the same row to be drawn more than once. Default is `False`.
```python
df.sample(n=5, replace=True)
```

---

# ⚡ Industry Best Practices

✅ **Test on Samples First**: If you write a complex Pandas `.apply()` function that takes 30 minutes to run on 10 million rows, test it on `df.sample(1000)` first to ensure it doesn't crash.
✅ **Always set `random_state` in ML**: When splitting data for training and testing, you use random sampling. Always set `random_state` so your model results are reproducible by other engineers.

---

# 💼 Interview Questions

### Q1. What is the difference between `head()`, `tail()`, and `sample()`?
`head()` returns the first rows, `tail()` returns the last rows, and `sample()` returns randomly selected rows.

### Q2. How do you select exactly 25% of your DataFrame randomly?
`df.sample(frac=0.25)`

### Q3. Why is `random_state` important?
It seeds the random number generator, ensuring that the same random rows are selected every time the script is run, which is vital for reproducibility and debugging.

---

# 🧠 Engineer Thinking

When reviewing `sample()`, ask yourself:
- Do the random rows have missing values (`NaN`) that weren't present in `head()`?
- Is there variance in the categorical columns (e.g., different cities, different statuses) in the random sample?

---

# 📌 Summary

- `sample()` provides an unbiased look at your data.
- Use `n` for a specific count, `frac` for a percentage.
- Always use `random_state` when you need reproducibility.

---

# 🚀 What's Next?

The next topic is:

**[04-info().md](04-info().md)**

You will learn how to view the technical metadata of your DataFrame, such as data types and missing value counts.
