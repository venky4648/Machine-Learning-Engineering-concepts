# 🗜️ Reading Parquet Files in Pandas

> As datasets grow from Gigabytes to Terabytes, CSV becomes too slow and takes up too much space. Apache Parquet is the industry standard for big data storage. Every Machine Learning Engineer working with Data Lakes or Big Data uses Parquet.

---

# 📖 Table of Contents

1. Introduction
2. What is Parquet?
3. Why Do Companies Use Parquet?
4. Installing Required Libraries
5. Reading Parquet Files
6. Important Parameters
7. CSV vs Parquet
8. Industry Best Practices
9. Interview Questions
10. Summary

---

# 🎯 Learning Objectives

After completing this topic, you will be able to:

- Understand columnar storage formats.
- Explain the advantages of Parquet over CSV.
- Load Parquet files efficiently using Pandas.
- Filter columns during load for massive performance gains.

---

# 📘 What is Parquet?

Apache Parquet is an open-source, **column-oriented** data file format designed for efficient data storage and retrieval.

Unlike CSV, which stores data row-by-row, Parquet stores data column-by-column. It also includes the schema (data types) and built-in compression.

---

# 🏢 Why Do Companies Use Parquet?

- **Massive Compression**: It compresses data incredibly well, reducing storage costs on AWS/GCP significantly.
- **Speed**: Because it's columnar, reading specific columns (which is common in ML) is blazingly fast.
- **Schema Preservation**: Parquet remembers data types. You don't have to specify `dtype` or `parse_dates` every time you load the file.
- **Big Data Ecosystem**: It is the default format for Hadoop, Spark, AWS Athena, and Snowflake.

---

# 📦 Installing Required Libraries

Pandas requires an engine to read Parquet files. The most common is `pyarrow`.

```bash
pip install pyarrow fastparquet pandas
```

---

# 📂 Reading a Parquet File

```python
import pandas as pd

# Reads the entire parquet file
df = pd.read_parquet("data.parquet")
```

---

# ⚙️ Important Parameters

## 1. columns

Because Parquet is columnar, you can load only the columns you need. This skips reading the other columns from disk entirely (unlike CSV, where the whole row is read anyway).

```python
df = pd.read_parquet(
    "data.parquet",
    columns=["user_id", "purchase_amount"]
)
```
*This is the biggest superpower of Parquet.*

## 2. engine

Specify the engine (`pyarrow` or `fastparquet`). Usually, `pyarrow` is the default and preferred for its speed.

```python
df = pd.read_parquet("data.parquet", engine="pyarrow")
```

---

# ⚖️ CSV vs Parquet

| Feature | CSV | Parquet |
|---------|-----|---------|
| **Storage Type** | Row-based | Columnar |
| **Compression** | Poor/None | Excellent |
| **Read Speed (Subset of cols)** | Slow | Extremely Fast |
| **Keeps Data Types?** | No | Yes |
| **Human Readable?** | Yes | No (Binary format) |

---

# ⚡ Performance Tips

✅ **Always use Parquet for intermediate data**: When cleaning data and saving it for the next step in your ML pipeline, save it as Parquet, not CSV.
✅ **Select columns**: Only load the columns your model needs.
✅ **Partitioning**: In big data, Parquet files are often saved in partitioned folders (e.g., `/year=2023/month=01/`). Pandas can read partitioned datasets natively with `pyarrow`.

---

# 💼 Interview Questions

### Q1. What is the difference between row-oriented and column-oriented storage?
Row-oriented (CSV) stores all fields of a record together. Column-oriented (Parquet) stores all values of a single column together. Columnar is faster for analytical queries (like ML) where you only need a subset of columns across millions of rows.

### Q2. Why should you prefer Parquet over CSV for Machine Learning pipelines?
Parquet provides faster read times, requires significantly less disk space due to compression, and preserves data types automatically.

### Q3. Which library does Pandas use under the hood to read Parquet?
Usually `pyarrow` (Apache Arrow) or `fastparquet`.

---

# 🧠 Engineer Thinking

When dealing with large datasets, ask yourself:
- "Why am I waiting 5 minutes for this CSV to load?" -> *Convert it to Parquet once, and it will load in seconds next time.*
- "Am I losing my pandas data types (like datetime or categoricals) every time I save?" -> *Parquet preserves schema.*

---

# 📌 Summary

- Parquet is a columnar binary format optimized for Big Data.
- Use `pd.read_parquet()` with the `pyarrow` engine.
- Always use the `columns` parameter when you don't need all features.
- Switch from CSV to Parquet for any dataset over a few hundred Megabytes.

---

# 🚀 What's Next?

The next topic is:

**07-Text.md**

You'll learn how to read raw and structured text files, useful when dealing with logs or uncommon delimiters.
