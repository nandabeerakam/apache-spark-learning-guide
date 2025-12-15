---
title: Spark Architecture
nav_order: 3
---

# Spark Architecture: Driver, Executors, Cluster Managers

## 1. Spark Application Anatomy

A Spark application typically consists of:
- Driver program: Your main Python script or notebook that uses `SparkSession`.
- Cluster manager: Allocates resources to Spark (e.g., YARN, Kubernetes, standalone, Databricks).
- Executors: JVM processes on worker nodes that run tasks and hold cached data.

The driver coordinates work, while executors perform the actual computations.

## 2. Jobs, Stages, and Tasks

When the driver triggers an action:
- Job: Represents a high-level computation triggered by an action (`count()`, `show()`, `write`, etc.).
- Stage: Spark splits the job into stages separated by shuffles (data redistribution).
- Task: Each stage is further divided into tasks, one per partition, executed on executors.

Understanding this breakdown helps you interpret the Spark UI and tune performance (e.g., number of partitions).

## 3. Cluster Modes and Deployment

You can run Spark in different modes:
- Local mode: All components run on your machine, specified by `master("local[*]")`.
- Client mode (cluster): Driver runs on your machine, executors on cluster nodes.
- Cluster mode: Driver and executors both run within the cluster.

In local development, you usually start with local mode and later move to a cluster (YARN, Kubernetes, Databricks, EMR, Dataproc, etc.).

## 4. Example: Inspecting Master and App Name

from pyspark.sql import SparkSession

spark = SparkSession.builder
.appName("architecture-demo")
.master("local") ​
.getOrCreate()

sc = spark.sparkContext

print("App Name:", sc.appName)
print("Master :", sc.master)

spark.stop()


This simple script shows how the driver configures the Spark application. In cluster setups, the master URL points to the cluster manager instead of `local`.
