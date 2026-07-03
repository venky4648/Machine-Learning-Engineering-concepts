# 🥒 Reading Pickle Files in Pandas

> Pickling is Python's built-in way to serialize and deserialize objects. While you shouldn't use it for sharing data publicly, it is extremely common for temporarily saving processed DataFrames or trained Machine Learning models locally.

---

# 📖 Table of Contents

1. What is Pickle?
2. Why Use Pickle?
3. Reading Pickle Data
4. Security Warning!
5. Summary

---

# 🎯 Learning Objectives

After completing this topic, you will be able to:
- Understand Python object serialization.
- Save and load DataFrames using Pickle.
- Understand the security risks associated with Pickle.

---

# 📘 What is Pickle?

Pickle converts a Python object (like a Pandas DataFrame, a dictionary, or a Scikit-Learn model) into a binary byte stream. This stream can be saved to a `.pkl` file.

---

# 🏢 Why Use Pickle?

- **Exact State Preservation**: When you save a DataFrame to CSV, you lose categorical data types, datetime objects, and custom Python objects. Pickle saves the DataFrame *exactly* as it is in RAM.
- **Speed**: It is faster than CSV for saving/loading intermediate processing steps.
- **Models**: It is the default format for saving trained `scikit-learn` models.

---

# 📂 Using Pickle in Pandas

### Saving to Pickle
```python
import pandas as pd

# Assume df is heavily processed with specific datatypes
df.to_pickle("processed_data.pkl")
```

### Reading from Pickle
```python
df = pd.read_pickle("processed_data.pkl")
# The dataframe is exactly as it was, with all dtypes preserved!
```

---

# ⚠️ SECURITY WARNING

**Never unpickle data from an untrusted source.**

Pickle files can execute arbitrary malicious code upon loading. Unlike CSV or JSON, which are just data, a Pickle file can instruct Python to run system commands. 

Only use Pickle for your own internal intermediate files. If you need to share data safely while preserving schema, use **Parquet**.

---

# 📌 Summary

- Pickle is Python-specific object serialization.
- Use `pd.read_pickle()` and `df.to_pickle()` for exact state preservation.
- It is fast and retains all pandas metadata (dtypes, indexes).
- **Security Risk:** Never load `.pkl` files from untrusted sources. Prefer Parquet for sharing data.

---

# 🚀 What's Next?

The next topic is:

**10-Cloud.md**

You'll learn how to read data directly from cloud storage buckets (AWS S3, Google Cloud Storage), which is how data is accessed in real-world scalable cloud infrastructures.
