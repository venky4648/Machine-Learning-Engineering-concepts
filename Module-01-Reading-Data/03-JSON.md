# 📦 Reading JSON Files in Pandas

> JSON (JavaScript Object Notation) is one of the most commonly used data formats for APIs, web applications, cloud services, and Machine Learning pipelines. Understanding how to read and work with JSON data is an essential skill for every Machine Learning Engineer.

---

# 📖 Table of Contents

1. Introduction
2. What is JSON?
3. Why Do Companies Use JSON?
4. JSON Structure
5. Reading JSON Files
6. Reading Nested JSON
7. Important Parameters
8. Reading JSON from APIs
9. Industry Best Practices
10. Common Errors
11. Interview Questions
12. Summary

---

# 🎯 Learning Objectives

After completing this topic, you will be able to:

- Understand JSON structure.
- Read JSON files using Pandas.
- Handle nested JSON data.
- Read JSON data from APIs.
- Work with JSON in real-world Machine Learning projects.

---

# 📘 What is JSON?

JSON (JavaScript Object Notation) is a lightweight data-interchange format.

It stores data as **key-value pairs**.

Example:

```json
{
    "Employee_ID": 101,
    "Name": "Ram",
    "Age": 25,
    "Department": "IT"
}
```

Unlike CSV, JSON can represent:

- Nested objects
- Arrays
- Dictionaries
- Hierarchical data

---

# 🏢 Why Do Companies Use JSON?

JSON is the standard format used by:

- REST APIs
- Web Applications
- Mobile Applications
- Cloud Platforms
- Machine Learning APIs
- Microservices

Popular platforms returning JSON data:

- GitHub API
- Twitter/X API
- Weather APIs
- Google APIs
- OpenAI APIs

---

# 📂 Example JSON File

employees.json

```json
[
    {
        "Employee_ID": 101,
        "Name": "Ram",
        "Age": 25,
        "Department": "IT"
    },
    {
        "Employee_ID": 102,
        "Name": "Ravi",
        "Age": 28,
        "Department": "HR"
    },
    {
        "Employee_ID": 103,
        "Name": "John",
        "Age": 30,
        "Department": "Finance"
    }
]
```

---

# 📥 Import Pandas

```python
import pandas as pd
```

---

# 📖 Reading a JSON File

```python
import pandas as pd

df = pd.read_json("employees.json")
```

---

Output

```text
   Employee_ID  Name  Age Department
0          101   Ram   25         IT
1          102  Ravi   28         HR
2          103  John   30    Finance
```

---

# ⚙️ Important Parameters

## 1. orient

Specifies how JSON data is organized.

```python
pd.read_json(
    "employees.json",
    orient="records"
)
```

Common values:

- records
- columns
- index
- split
- values

---

## 2. dtype

Specify column data types.

```python
df = pd.read_json(
    "employees.json",
    dtype={
        "Employee_ID": int,
        "Age": int
    }
)
```

---

## 3. convert_dates

Automatically convert date columns.

```python
df = pd.read_json(
    "employees.json",
    convert_dates=True
)
```

---

## 4. encoding

Specify file encoding.

```python
pd.read_json(
    "employees.json",
    encoding="utf-8"
)
```

---

# 🏗️ Reading Nested JSON

Example

```json
[
    {
        "Name": "Ram",
        "Address": {
            "City": "Hyderabad",
            "State": "Telangana"
        }
    }
]
```

Using only `read_json()` keeps the nested object as a dictionary.

To flatten nested JSON, use:

```python
import pandas as pd

df = pd.json_normalize(data)
```

Output

```text
Name    Address.City    Address.State

Ram     Hyderabad       Telangana
```

`pd.json_normalize()` is especially useful when working with API responses.

---

# 🌐 Reading JSON from an API

Example:

```python
import pandas as pd

url = "https://api.example.com/employees"

df = pd.read_json(url)
```

In real projects, APIs are often accessed using the `requests` library.

Example:

```python
import requests
import pandas as pd

response = requests.get("https://api.example.com/employees")

data = response.json()

df = pd.DataFrame(data)
```

This approach gives you more control over authentication, headers, and error handling.

---

# 🏢 Real Industry Example

An HR Management System provides an API:

```json
[
    {
        "Employee_ID":101,
        "Name":"Ram",
        "Department":"IT"
    }
]
```

Instead of downloading a CSV every day, your ML pipeline fetches fresh employee data directly from the API and converts it into a Pandas DataFrame.

---

# ⚡ Performance Tips

- Read only the required JSON files.
- Flatten nested JSON before analysis.
- Convert data types after loading if necessary.
- Validate JSON structure before processing.
- For very large JSON files, consider chunk-based or streaming approaches.

---

# ❌ Common Mistakes

### Mistake 1

Assuming every JSON file has the same structure.

Different APIs may return different formats.

---

### Mistake 2

Ignoring nested objects.

Nested dictionaries cannot always be analyzed directly.

Use:

```python
pd.json_normalize()
```

---

### Mistake 3

Not validating API responses.

Always verify that the API returned the expected data before processing.

---

### Mistake 4

Forgetting to handle missing keys.

Some JSON records may not contain all fields.

---

# 💼 Interview Questions

### Q1. What is JSON?

JSON is a lightweight data-interchange format that stores information using key-value pairs.

---

### Q2. Which Pandas function reads JSON files?

```python
pd.read_json()
```

---

### Q3. Which function flattens nested JSON?

```python
pd.json_normalize()
```

---

### Q4. Why is JSON preferred for APIs?

Because it is lightweight, human-readable, language-independent, and supports nested structures.

---

### Q5. Can Pandas directly read JSON from a URL?

Yes.

```python
pd.read_json(url)
```

However, for production applications, using the `requests` library is generally recommended.

---

# 🧠 Engineer Thinking

When working with JSON, ask yourself:

- Is the JSON flat or nested?
- Is every record consistent?
- Are all expected keys present?
- Should nested objects be flattened?
- Am I reading data from a file or an API?
- Do I need authentication to access the API?

These questions help ensure your data pipeline is reliable and scalable.

---

# 📌 CSV vs Excel vs JSON

| Feature | CSV | Excel | JSON |
|---------|-----|-------|------|
| Human Readable | ✅ | ✅ | ✅ |
| Nested Data | ❌ | ❌ | ✅ |
| Multiple Sheets | ❌ | ✅ | ❌ |
| API Friendly | ❌ | ❌ | ✅ |
| Lightweight | ✅ | ❌ | ✅ |
| Machine Learning | ✅ | ✅ | ✅ |

---

# 📌 Summary

- JSON stores data as key-value pairs.
- Use `pd.read_json()` to read JSON files.
- Use `pd.json_normalize()` to flatten nested JSON.
- APIs commonly return JSON responses.
- Validate JSON structure before analysis.
- Understand whether the data is flat or nested before processing.

---

# 🚀 What's Next?

The next topic is:

**04-SQL.md**

You'll learn how to connect to databases, execute SQL queries, and load data directly into Pandas DataFrames—a core skill for Machine Learning Engineers working with production databases.