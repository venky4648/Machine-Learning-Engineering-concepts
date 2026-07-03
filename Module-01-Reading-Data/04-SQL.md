# 🗄️ Reading Data from SQL in Pandas

> SQL databases (Relational Database Management Systems) are the backbone of most enterprise data architectures. As a Machine Learning Engineer, you will often need to connect to databases, run SQL queries, and load the results directly into Pandas for analysis and modeling.

---

# 📖 Table of Contents

1. Introduction
2. What is SQL?
3. Why Do Companies Use SQL?
4. Installing Required Libraries
5. Connecting to a Database
6. Reading Data using Pandas
7. Reading Specific Tables and Queries
8. Industry Best Practices
9. Common Errors
10. Interview Questions
11. Summary

---

# 🎯 Learning Objectives

After completing this topic, you will be able to:

- Understand the importance of SQL in ML workflows.
- Connect Pandas to SQL databases (MySQL, PostgreSQL, SQLite).
- Execute SQL queries and load data directly into DataFrames.
- Use `pd.read_sql()`, `pd.read_sql_query()`, and `pd.read_sql_table()`.
- Handle common database connection issues safely.

---

# 📘 What is SQL?

SQL (Structured Query Language) is the standard language for managing and querying relational databases.

Data in SQL is organized into tables with rows and columns, similar to Excel or CSV, but optimized for scale, consistency, and complex relationships.

---

# 🏢 Why Do Companies Use SQL?

Companies use SQL databases for:

- **Data Integrity**: Ensures data is accurate and consistent.
- **Scalability**: Can handle millions of rows efficiently.
- **Security**: Robust access control and user management.
- **Transactions**: Supports ACID properties for reliable operations.

Most real-world ML models are trained on data extracted from enterprise SQL databases or Data Warehouses.

---

# 📦 Installing Required Libraries

To connect Pandas to a SQL database, you typically need an Engine (like SQLAlchemy) and a Driver (like `psycopg2` for PostgreSQL or `pymysql` for MySQL).

```bash
pip install sqlalchemy
# For SQLite (built-in, no driver needed)
# For PostgreSQL: pip install psycopg2
# For MySQL: pip install pymysql
```

---

# 🔌 Connecting to a Database

We use **SQLAlchemy** to create a connection engine.

```python
import pandas as pd
from sqlalchemy import create_engine

# SQLite example
engine = create_engine('sqlite:///company.db')

# PostgreSQL example
# engine = create_engine('postgresql://username:password@localhost:5432/mydatabase')

# MySQL example
# engine = create_engine('mysql+pymysql://username:password@localhost/mydatabase')
```

---

# 📖 Reading Data using Pandas

## 1. `pd.read_sql()`

The most versatile function. It can accept a table name or a raw SQL query.

```python
import pandas as pd
from sqlalchemy import create_engine

engine = create_engine('sqlite:///company.db')

# Passing a table name
df = pd.read_sql("employees", engine)
```

## 2. `pd.read_sql_query()`

Specifically for executing a SQL query. This is preferred in industry because it allows filtering data *before* loading it into memory.

```python
query = """
SELECT Employee_ID, Name, Salary 
FROM employees 
WHERE Department = 'IT' AND Salary > 50000;
"""

df = pd.read_sql_query(query, engine)
```

## 3. `pd.read_sql_table()`

Specifically for loading an entire table. (Requires SQLAlchemy).

```python
df = pd.read_sql_table("employees", engine, columns=["Name", "Department"])
```

---

# ⚡ Performance Tips

✅ **Filter in SQL, not in Pandas**: Always use `WHERE` clauses in your SQL queries to limit data. Don't `SELECT *` and then filter in Pandas.
✅ **Select only required columns**: Avoid `SELECT *`. Explicitly list the columns you need.
✅ **Use chunking**: For massive tables, load data in chunks.

```python
# Reading in chunks of 10,000 rows
chunks = pd.read_sql_query("SELECT * FROM large_table", engine, chunksize=10000)

for chunk in chunks:
    # process chunk
    pass
```

---

# ❌ Common Mistakes

### Mistake 1

Hardcoding passwords in your scripts.

```python
# Bad practice!
engine = create_engine('postgresql://admin:supersecret123@localhost/db')
```

**Solution**: Use environment variables (`os.environ`) or `.env` files.

### Mistake 2

Loading an entire table into memory when only a subset is needed. Pandas stores data in RAM; SQL engines process data on disk. Always push filtering down to the database.

---

# 💼 Interview Questions

### Q1. How do you load SQL data into Pandas?
Using `pd.read_sql()` or `pd.read_sql_query()` along with a SQLAlchemy engine connection.

### Q2. What is the difference between `read_sql`, `read_sql_query`, and `read_sql_table`?
- `read_sql` is a convenience wrapper around both.
- `read_sql_query` explicitly takes a SQL query string.
- `read_sql_table` explicitly takes a table name and requires SQLAlchemy.

### Q3. How do you handle reading a table that is larger than your system's RAM?
By using the `chunksize` parameter in `pd.read_sql_query()` to read and process the data in manageable batches.

---

# 🧠 Engineer Thinking

When reading from SQL, ask yourself:
- Do I really need all the columns?
- Can I do the aggregation/filtering in SQL to save memory?
- Are my database credentials secure?
- Is my query optimized with proper indexes in the database?

---

# 📌 Summary

- SQL is the foundation of enterprise data.
- Use `SQLAlchemy` to create a secure, reliable connection engine.
- Prefer `pd.read_sql_query()` to filter data at the database level.
- Handle large datasets using `chunksize`.
- Never hardcode database credentials.

---

# 🚀 What's Next?

The next topic is:

**05-API.md**

You'll learn how to read data dynamically from web APIs, an essential skill for acquiring real-time data or integrating with modern cloud services.
