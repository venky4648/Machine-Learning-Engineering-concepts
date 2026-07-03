# 📝 Reading XML Files in Pandas

> XML (eXtensible Markup Language) was the standard for data interchange before JSON took over. However, it remains heavily used in enterprise systems, SOAP APIs, finance, and government open data.

---

# 📖 Table of Contents

1. What is XML?
2. Reading XML Files
3. Important Parameters
4. Using XPath
5. Summary

---

# 🎯 Learning Objectives

After completing this topic, you will be able to:
- Understand XML tree structures.
- Use `pd.read_xml()` to parse XML into DataFrames.
- Use XPath to navigate and extract specific XML nodes.

---

# 📘 What is XML?

XML looks similar to HTML. It uses custom tags to define data structures hierarchically.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<Company>
    <Employee>
        <ID>101</ID>
        <Name>Ram</Name>
        <Department>IT</Department>
    </Employee>
    <Employee>
        <ID>102</ID>
        <Name>Ravi</Name>
        <Department>HR</Department>
    </Employee>
</Company>
```

---

# 📂 Reading XML Files

Pandas added `read_xml()` in version 1.3.0.

```python
import pandas as pd

df = pd.read_xml("employees.xml")
```

Output:
```text
    ID  Name Department
0  101   Ram         IT
1  102  Ravi         HR
```

---

# 🗺️ Using XPath

If your XML file is deeply nested and you only want a specific subset of the data, you can use **XPath** (XML Path Language).

```python
# Assuming the XML has nested <Department> tags
df = pd.read_xml("company_data.xml", xpath=".//Employee")
```

XPath allows you to precisely target the nodes that represent the rows of your desired DataFrame.

---

# 📌 Summary

- XML is a tag-based hierarchical format.
- Use `pd.read_xml()` to easily load simple XML structures.
- For complex, nested XML, utilize the `xpath` parameter to target the correct data layer.

---

# 🚀 What's Next?

The next topic is:

**09-Pickle.md**

You'll learn about Python's native serialization format, Pickle, which is heavily used for saving and loading Machine Learning models and complex Python objects.
