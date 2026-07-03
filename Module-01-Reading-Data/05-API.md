# 🌐 Reading Data from APIs

> APIs (Application Programming Interfaces) are how modern applications communicate. Whether it's fetching weather data, stock prices, or real-time inferences from a microservice, consuming APIs is a core skill for any Data or ML professional.

---

# 📖 Table of Contents

1. Introduction
2. What is an API?
3. Why Use APIs?
4. Using the `requests` library
5. Converting API Data to Pandas
6. Handling Pagination and Limits
7. Industry Best Practices
8. Common Errors
9. Interview Questions
10. Summary

---

# 🎯 Learning Objectives

After completing this topic, you will be able to:

- Understand REST APIs and JSON responses.
- Fetch data from APIs using Python's `requests` library.
- Convert complex, nested API responses into Pandas DataFrames.
- Handle API pagination, authentication, and rate limits safely.

---

# 📘 What is an API?

An API (Application Programming Interface) allows two software programs to communicate. A Web API (typically REST) allows you to send an HTTP request to a server and receive data back, usually in JSON format.

---

# 🏢 Why Do Companies Use APIs?

- **Real-time Data**: Get up-to-the-second data (e.g., stock tickers).
- **Service Integration**: Pull data from tools like Salesforce, Jira, or Google Analytics.
- **Microservices Architecture**: Models often request features from a feature store API.
- **Standardization**: Provides a clean interface to underlying databases without granting direct SQL access.

---

# 📦 Installing Required Libraries

Pandas has `read_json`, but for robust API interaction (headers, auth, parameters), the `requests` library is the industry standard.

```bash
pip install requests pandas
```

---

# 🔌 Fetching API Data

Let's use a public API to fetch user data.

```python
import requests
import pandas as pd

# Define the endpoint
url = "https://jsonplaceholder.typicode.com/users"

# Send a GET request
response = requests.get(url)

# Check if the request was successful (Status Code 200)
if response.status_code == 200:
    # Parse the JSON response
    data = response.json()
    
    # Convert to a DataFrame
    df = pd.DataFrame(data)
    print(df.head())
else:
    print(f"Failed to retrieve data. Status code: {response.status_code}")
```

---

# 🏗️ Handling Nested API Data

APIs often return deeply nested JSON. `pd.DataFrame()` might leave dictionaries in your columns.

```python
# Normalizing nested JSON
df_normalized = pd.json_normalize(data)
```

This expands nested keys like `address.city` into separate columns, making it ready for ML.

---

# 🔄 Handling Pagination

Many APIs limit the number of records returned per request (e.g., 100 per page). You must "page" through the results.

```python
all_data = []
page = 1

while True:
    res = requests.get(f"https://api.example.com/data?page={page}")
    data = res.json()
    
    if not data: # Break if no more data is returned
        break
        
    all_data.extend(data)
    page += 1

df = pd.DataFrame(all_data)
```

---

# ⚡ Performance Tips

✅ **Respect Rate Limits**: APIs often have limits (e.g., 60 requests/minute). Use `time.sleep()` to avoid getting blocked.
✅ **Use Sessions**: If making multiple requests to the same host, use `requests.Session()` to reuse the underlying TCP connection and improve speed.
✅ **Handle Timeouts**: Always set a timeout to prevent your script from hanging indefinitely: `requests.get(url, timeout=10)`.

---

# ❌ Common Mistakes

### Mistake 1: Exposing API Keys

```python
# NEVER do this
api_key = "12345-abcde-secret-key"
```
**Solution**: Use `.env` files or environment variables.

### Mistake 2: Ignoring Status Codes

Assuming the API always works. If the API returns a 500 error, calling `.json()` will fail. Always check `response.status_code == 200`.

---

# 💼 Interview Questions

### Q1. How do you retrieve data from a REST API in Python?
Using the `requests` library to send a `GET` request, parsing the response using `.json()`, and converting it to a DataFrame using `pd.DataFrame()` or `pd.json_normalize()`.

### Q2. How do you deal with nested JSON structures from an API?
Using `pd.json_normalize()`, which flattens the nested dictionaries into standard relational columns.

### Q3. What is API Pagination and how do you handle it?
Pagination is when an API splits large datasets across multiple "pages". It is handled by writing a loop that repeatedly requests the next page until no more data is returned.

---

# 🧠 Engineer Thinking

When working with APIs, ask yourself:
- How often do I need to poll this API? Can I cache the results?
- What happens if the API goes down or changes its schema?
- Am I securely storing my API tokens?
- Is there a bulk download endpoint instead of paginating through thousands of records?

---

# 📌 Summary

- APIs are the standard way to retrieve data over the web.
- Use `requests` for robust HTTP interactions (handling auth, headers, timeouts).
- Use `pd.json_normalize()` to flatten nested responses.
- Always check status codes and handle pagination and rate limits defensively.

---

# 🚀 What's Next?

The next topic is:

**06-Parquet.md**

You'll learn about Parquet, the highly optimized, columnar storage format that powers modern Big Data and Data Lake architectures.
