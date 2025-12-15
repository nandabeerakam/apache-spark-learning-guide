---
title: Spark Ecosystem and Components
nav_order: 2
---

# Spark Ecosystem and Components

## 1. Spark Core

Spark Core is the fundamental execution engine of Spark. It provides:
- Task scheduling and distribution.
- Memory management and caching.
- Fault tolerance through lineage (recomputing lost partitions).
- Low-level RDD API (Resilient Distributed Datasets).

Most higher-level APIs (DataFrames, SQL, Streaming, MLlib) ultimately run on top of Spark Core.

## 2. Spark SQL (DataFrames and SQL)

Spark SQL provides:
- DataFrame API: A distributed table-like abstraction with named columns.
- SQL engine: You can run SQL queries over DataFrames and external tables.
- Catalyst optimizer and Tungsten execution engine to optimize query plans and physical execution.

Example in PySpark:

from pyspark.sql import SparkSession

spark = SparkSession.builder.appName("spark-sql-demo").getOrCreate()

data = [("alice", 23), ("bob", 30)]
df = spark.createDataFrame(data, ["name", "age"])

df.createOrReplaceTempView("people")

result = spark.sql("""
SELECT name, age
FROM people
WHERE age >= 25
""")

result.show()

## 3. Spark Structured Streaming

Structured Streaming treats a stream of data as an unbounded table. New data is incrementally appended, and Spark continuously updates the results of your queries.

Typical use cases:
- Real-time dashboards for log or clickstream data.
- Fraud detection streams.
- Near real-time data pipelines feeding downstream systems.

## 4. Spark MLlib

MLlib is Spark’s library for scalable machine learning. It provides:
- Feature transformers (e.g., tokenizers, vector assemblers).
- Algorithms (logistic regression, random forests, k-means, etc.).
- Pipeline API for chaining transformations and models.

Example skeleton (details later in dedicated MLlib page):

from pyspark.ml.feature import VectorAssembler
from pyspark.ml.classification import LogisticRegression

assembler = VectorAssembler(inputCols=["feature1", "feature2"], outputCol="features")
lr = LogisticRegression(featuresCol="features", labelCol="label")


## 5. Other Components (GraphX and Connectors)

- GraphX: Graph processing library, primarily used with Scala/Java.
- Connectors: Spark integrates with many systems (Kafka, JDBC databases, cloud storage like S3/ADLS/GCS).

As a PySpark-focused beginner, you primarily deal with Spark SQL/DataFrames and Structured Streaming, plus occasional MLlib usage.
