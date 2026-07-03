# 💾 memory_usage() in Pandas

> `memory_usage()` reveals exactly how much RAM each column in your dataset consumes. In Big Data, running out of memory (OOM crashes) is a common hurdle, making this function a vital optimization tool for engineers.

---

# 📖 Table of Contents

1. Introduction
2. Learning Objectives
3. What is `memory_usage()`?
4. Why Do We Use `memory_usage()`?
5. Syntax
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

- Determine the memory footprint of a DataFrame.
- Differentiate between shallow and deep memory calculation.
- Identify the most expensive columns in your dataset.

---

# 📘 What is `memory_usage()`?

The `memory_usage()` function returns the memory usage of each column in bytes. 

It provides a more granular view than `info()`, allowing you to see exactly which features are eating up your computer's RAM.

---

# ❓ Why Do We Use `memory_usage()`?

Pandas processes data entirely in RAM. If you try to load a 10GB CSV file into a laptop with 8GB of RAM, your system will crash.

Using `memory_usage()` helps you:

- **Identify Bloat**: Find out which columns take the most space.
- **Optimize Data Types**: Realize that converting a 64-bit float to a 32-bit float cuts memory in half.
- **Convert Text**: Realize that converting `object` strings to `category` types saves massive amounts of space.

---

# 📝 Syntax

```python
DataFrame.memory_usage(
    index=True,
    deep=False
)
```

---

# ⚙️ Parameters

| Parameter | Description | Default |
|-----------|-------------|---------|
| `index` | Whether to include the memory usage of the DataFrame's index. | `True` |
| `deep` | If `True`, introspects the data deeply to calculate the exact memory of `object` (string) types. | `False` |

---

# 💻 Example Dataset

```text
Employee_ID   Department      Notes
101           IT              Has worked here for 5 years...
102           HR              Recently promoted...
103           IT              Transferred from another branch...
```

---

# 📌 Example 1 – Default Behavior

```python
import pandas as pd

df = pd.read_csv("employees.csv")

print(df.memory_usage())
```

### Output

```text
Index         128
Employee_ID   800
Department    800
Notes         800
dtype: int64
```
*Wait, why do text columns and integer columns show the same memory usage?* Because `deep=False` only checks the memory of the pointers, not the actual text strings!

---

# 📌 Example 2 – Deep Memory Inspection

To get the *true* memory footprint of text data, use `deep=True`.

```python
print(df.memory_usage(deep=True))
```

### Output

```text
Index           128
Employee_ID     800
Department     3200
Notes         45000
dtype: int64
```
Now you see the truth: the `Notes` column is taking up significantly more memory than the integers.

---

# 📌 Example 3 – Total Memory Calculation

To find the total memory used by the entire DataFrame in Megabytes:

```python
total_memory_mb = df.memory_usage(deep=True).sum() / (1024 ** 2)
print(f"Total Memory: {total_memory_mb:.2f} MB")
```

---

# 🏢 Real Industry Example

A Data Engineer is processing a log file with 50 million rows on an AWS EC2 instance. The script keeps crashing with an "Out of Memory" error.

They load a small sample and use `memory_usage(deep=True)`. They discover a string column called `Country` is consuming 2GB of RAM.

They optimize the script to load `Country` as a `category` dtype instead of `object`. The memory usage for that column drops from 2GB to 50MB, and the script runs perfectly.

---

# 🧠 Engineer Thinking

When reviewing memory usage, ask yourself:

- Are there columns taking up GBs of RAM that I don't even need for my ML model? (Drop them).
- Can this `float64` column safely be downcast to `float32` without losing precision?
- Can this text column be converted to a category?

---

# ⚡ Performance Notes

- Running `memory_usage(deep=True)` on a massive dataset can be slow because Pandas has to inspect the length of every single string in the DataFrame.

---

# ✅ Best Practices

- Always use `deep=True` when dealing with `object` data types for an accurate measurement.
- If you have to process data larger than your RAM, use tools like `chunksize` in `read_csv`, or switch from Pandas to Polars or PySpark.

---

# ❌ Common Mistakes

### Mistake 1

Forgetting `deep=True`.

If you forget this, Pandas will drastically underestimate the memory used by string columns, giving you a false sense of security before an OOM crash.

---

### Mistake 2

Misinterpreting the output format.

The output is always in **bytes**. You must divide by `1024` for KB, `1024**2` for MB, and `1024**3` for GB.

---

# 💼 Interview Questions

### Q1. Why does `memory_usage()` underestimate memory for string columns by default?

Because by default (`deep=False`), Pandas only counts the memory occupied by the array of object pointers, not the varying lengths of the actual strings stored in memory.

---

### Q2. How do you drastically reduce the memory usage of a repetitive text column?

By converting the column's data type from `object` to `category`.

---

# 📌 Summary

- `memory_usage()` shows RAM consumption in bytes.
- It helps prevent out-of-memory crashes.
- Always use `deep=True` for accurate string memory calculations.
- Use `.sum()` to find the total DataFrame footprint.

---

# 🚀 Next Topic

The next topic is:

**11-unique().md**

You'll learn how to extract all distinct values from a column, a critical step for understanding categorical features.
