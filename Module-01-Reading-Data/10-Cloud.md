# ☁️ Reading Data from Cloud Storage

> In production ML environments, data does not live on your laptop. It lives in cloud object storage like AWS S3, Google Cloud Storage (GCS), or Azure Blob Storage. Learning to read data directly from the cloud is a mandatory MLOps skill.

---

# 📖 Table of Contents

1. Cloud Storage Overview
2. Installing Required Libraries
3. Reading from AWS S3
4. Reading from Google Cloud Storage (GCS)
5. Authentication and Security
6. Summary

---

# 🎯 Learning Objectives

After completing this topic, you will be able to:
- Understand object storage concepts.
- Read CSV/Parquet files directly from AWS S3 and GCS using Pandas.
- Handle cloud authentication securely.

---

# 📘 Cloud Storage Overview

Object storage allows companies to store massive amounts of unstructured or semi-structured data securely.

- **AWS**: Simple Storage Service (S3)
- **GCP**: Google Cloud Storage (GCS)
- **Azure**: Azure Blob Storage

Instead of downloading files locally to process them, Pandas can stream data directly from these URIs.

---

# 📦 Installing Required Libraries

Pandas relies on `fsspec` and specific file-system libraries to interact with the cloud.

```bash
# For AWS S3
pip install s3fs

# For Google Cloud Storage
pip install gcsfs
```

---

# 🟠 Reading from AWS S3

You can provide the `s3://` URI directly to your standard Pandas read functions.

```python
import pandas as pd

# Read CSV directly from an S3 bucket
df = pd.read_csv("s3://my-company-data-bucket/sales_2023.csv")

# Read Parquet directly from an S3 bucket
df_parquet = pd.read_parquet("s3://my-company-data-bucket/features.parquet")
```

---

# 🔵 Reading from Google Cloud Storage

Similarly, for GCS, use the `gs://` URI.

```python
import pandas as pd

# Read from a GCS bucket
df = pd.read_csv("gs://my-gcp-data-bucket/marketing_data.csv")
```

---

# 🔐 Authentication and Security

By default, these commands will only work if the bucket is public, which is **never** the case for company data. 

You must authenticate your environment:

### For AWS S3:
Configure your AWS credentials locally using the AWS CLI:
```bash
aws configure
```
This stores your Access Keys in `~/.aws/credentials`. `s3fs` automatically picks them up.

### For GCP GCS:
Set the environment variable pointing to your service account JSON key:
```bash
export GOOGLE_APPLICATION_CREDENTIALS="/path/to/keyfile.json"
```

---

# 🧠 Engineer Thinking

When reading from the cloud:
- **Cost**: Cloud egress (downloading data out of the cloud) costs money. Run your code in the same cloud region as your data bucket (e.g., run your EC2 instance in `us-east-1` if your S3 bucket is in `us-east-1`).
- **Memory**: Do not pull a 50GB CSV file from S3 into memory. Use cloud-native query tools like AWS Athena to filter the data first, or read Parquet files by specifying specific columns.

---

# 📌 Summary

- Pandas can read data directly from cloud URIs (`s3://`, `gs://`).
- You must install the respective drivers (`s3fs`, `gcsfs`).
- Secure your connections using standard CLI auth tools and never hardcode keys in your scripts.

---

# 🚀 What's Next?

Congratulations! You have completed **Module 01: Reading Data**.

You now know how to extract data from CSV, Excel, JSON, SQL Databases, APIs, Parquet, and the Cloud. 

The next step in the roadmap is **Module 02: Understanding Data**, where you will learn how to analyze the shape, structure, and basic statistics of the data you just loaded.
