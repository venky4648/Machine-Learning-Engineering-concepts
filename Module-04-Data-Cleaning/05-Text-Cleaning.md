# 🔤 Text Cleaning in Pandas

> Text data (Strings) entered by humans is notoriously messy. It contains random capitalizations, leading spaces, and weird punctuation. Standardizing this text is a mandatory step before categorical encoding or Natural Language Processing (NLP).

---

# 📖 Table of Contents

1. Introduction
2. Learning Objectives
3. What is Text Cleaning?
4. Why Do We Need It?
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

- Strip invisible whitespace from text columns.
- Standardize capitalization (lower, upper, title case).
- Replace or remove specific characters or substrings.
- Use basic Regular Expressions (Regex) for text replacement.

---

# 📘 What is Text Cleaning?

Text cleaning involves using Pandas String methods (accessed via `.str`) to sanitize `object` columns. It ensures that logically identical strings are mathematically identical to the computer.

---

# ❓ Why Do We Need It?

If a user types `"  New York "` and another types `"new york"`, a Machine Learning model treats these as two entirely different cities. 

If you apply One-Hot Encoding to this messy data, you will generate dozens of unnecessary, redundant columns that will severely degrade model performance.

---

# 📝 Syntax & Methods

Pandas provides a `.str` accessor to apply Python string methods to entire columns instantly.

```python
# Strip leading/trailing whitespace
df['Col'] = df['Col'].str.strip()

# Change casing
df['Col'] = df['Col'].str.lower()
df['Col'] = df['Col'].str.upper()

# Replace characters
df['Col'] = df['Col'].str.replace('old', 'new')
```

---

# ⚙️ Parameters

For `str.replace()`:

| Parameter | Description | Default |
|-----------|-------------|---------|
| `pat` | The string or regex pattern to find. | None |
| `repl` | The replacement string. | None |
| `regex` | If `True`, interprets `pat` as a regular expression. | `False` (usually) |

---

# 💻 Example Dataset

```text
ID    City
1       New York  
2     new york
3     NEW YORK!
4     Los Angeles
```

---

# 📌 Example 1 – Stripping Whitespace

Hidden spaces are a nightmare for joins and grouping.

```python
import pandas as pd

df = pd.DataFrame({'City': ['  New York  ', 'new york', 'NEW YORK!', 'Los Angeles']})

# Strip spaces
df['City'] = df['City'].str.strip()
```

---

# 📌 Example 2 – Standardizing Casing

```python
# Convert everything to lowercase
df['City'] = df['City'].str.lower()

print(df['City'].values)
```

### Output
```text
['new york' 'new york' 'new york!' 'los angeles']
```
Notice how the first two are now identical, but the third still has an exclamation mark.

---

# 📌 Example 3 – Removing Punctuation with Regex

```python
# Replace any non-word character (like punctuation) with nothing
df['City'] = df['City'].str.replace(r'[^\w\s]', '', regex=True)

print(df['City'].values)
```

### Output
```text
['new york' 'new york' 'new york' 'los angeles']
```
Now, the first three rows are perfectly uniform!

---

# 🏢 Real Industry Example

A Data Engineer is cleaning a `Phone_Number` column. Users have entered data like:
- `(555) 123-4567`
- `555.123.4567`
- `+1 555 123 4567`

The engineer chains string methods to strip everything except numbers:
```python
df['Phone'] = df['Phone'].str.replace(r'\D', '', regex=True)
```
*(The `\D` regex matches any non-digit character).* This instantly cleans 10 million rows, reducing all formats to a pure 10-digit number like `5551234567`.

---

# 🧠 Engineer Thinking

When looking at text data, ask yourself:

- Did I strip whitespace? (You should ALWAYS do this, even if the data looks clean).
- Is this column meant to be a categorical feature (like City)? If so, apply `.lower()` to group identical entities.
- Does the text contain nested symbols like currency signs (`$`, `€`) that prevent me from converting it to a float?

---

# ⚡ Performance Notes

- Pandas `.str` methods are convenient but generally slower than highly optimized NumPy mathematical operations because they operate in Python object space. If text cleaning becomes a massive bottleneck, engineers switch to vectorized regex libraries or tools like Polars.

---

# ✅ Best Practices

- Always chain `.str.strip().str.lower()` on any text column that will be treated as a category.
- When replacing exact strings, set `regex=False` for a performance boost.

---

# ❌ Common Mistakes

### Mistake 1

Forgetting `.str`.

```python
# Error!
df['City'] = df['City'].lower() 
```
`AttributeError: 'Series' object has no attribute 'lower'`. You must use `.str.lower()`.

---

### Mistake 2

Chaining too many `.str` operations without checking intermediate results. You might accidentally strip away valid characters (like an `@` in an email address) if your regex is too aggressive.

---

# 💼 Interview Questions

### Q1. How do you remove leading and trailing spaces from an entire DataFrame column?
By using `df['column'].str.strip()`.

---

### Q2. Why is converting text to lowercase important in ML?
Because Machine Learning models and group-by aggregations treat "Apple" and "apple" as two completely different categories. Lowercasing ensures uniform grouping.

---

### Q3. How do you replace a specific character inside a string column?
By using `df['column'].str.replace('old_char', 'new_char')`.

---

# 📌 Summary

- Text data must be standardized before encoding.
- Always use the `.str` accessor to apply string methods to Series.
- `.strip()` removes invisible padding.
- `.lower()` prevents case-sensitivity bugs.
- `regex=True` inside `.replace()` is incredibly powerful for complex cleaning.

---

# 🚀 Next Topic

The next topic is:

**06-Inconsistent-Data.md**

You'll learn how to map incorrect values and standardize categories (e.g., merging "USA" and "United States" into a single category).
