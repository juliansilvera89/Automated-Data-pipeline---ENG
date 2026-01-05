# 🚀 Automated Data Pipeline – End‑to‑End Project

## 📌 Overview

This project implements a **fully automated data pipeline** following real-world **Data Engineering best practices**. It covers the complete lifecycle of data: ingestion, transformation, storage in a Data Lake, loading into a Data Warehouse, SQL analytics, and **scheduled execution by run date**.

The project is designed to be **production-oriented**, reproducible, and easily migratable to tools like **Apache Airflow**.

---

## 🏗️ Architecture

```
Raw Data (CSV)
     ↓
Ingestion & Validation (Python)
     ↓
Transformations & Business Rules
     ↓
Data Lake (Parquet, partitioned by date)
     ↓
Data Warehouse (SQLite)
     ↓
SQL Analytics
     ↓
Scheduler (Daily execution simulation)
```

---

## 🧰 Tech Stack

* **Python 3**
* **Pandas** – data processing
* **PyArrow / Parquet** – analytical storage
* **SQLite** – lightweight Data Warehouse
* **Logging** – observability & monitoring
* **Google Colab** – execution environment

---

## 📁 Project Structure

```
data_pipeline/
├── data/
│   ├── raw/            # Raw and snapshot data (immutable)
│   ├── processed/      # Cleaned data in Parquet (Data Lake)
│   └── warehouse/      # SQLite Data Warehouse
├── logs/               # Pipeline & scheduler logs
├── scripts/            # (logical separation – merged in notebooks)
└── README.md
```

---

## 🔄 Pipeline Stages

### 1️⃣ Data Ingestion

* Reads raw CSV data
* Validates file existence and schema
* Prevents empty or corrupted loads
* Logs ingestion metrics

**Key principle:** Raw data is never modified.

---

### 2️⃣ Data Transformation

Applied business and data-quality rules:

* Date normalization and coercion
* Country and category standardization
* Price cleaning and numeric casting
* Quantity validation (no nulls or negatives)
* Duplicate removal by `order_id`
* Derived metric: `total_amount`

Output is stored in **Parquet format** for analytical workloads.

---

### 3️⃣ Data Lake (Processed Layer)

* Columnar storage (Parquet)
* One file per execution date (`run_date`)
* Enables historical backfills and reprocessing

Example:

```
orders_2024-01-01.parquet
orders_2024-01-02.parquet
orders_2024-01-03.parquet
```

---

### 4️⃣ Data Warehouse

* Clean data loaded into SQLite
* Fact table: `fact_orders`
* Ready for SQL analytics and BI tools

---

### 5️⃣ SQL Analytics

Example queries implemented:

* Total sales
* Sales by country
* Sales by product category
* Average ticket size

---

### 6️⃣ Automation & Scheduling

The pipeline is executed through a **single orchestrator function**, simulating a daily scheduler:

* Parameterized by `run_date`
* Supports historical backfills
* Logs each execution independently
* Fully idempotent

This design mirrors **Airflow DAG execution semantics**.

---

## 📊 Logging & Observability

* Centralized logs per pipeline and scheduler
* Clear START / SUCCESS / FAILURE states
* Timestamped execution history

Example log:

```
PIPELINE START - run_date=2024-01-02
INGEST - rows: 20000
TRANSFORM - parquet generated
DW - load completed
PIPELINE SUCCESS
```

---

## 🎯 Key Engineering Concepts Demonstrated

* ETL / ELT fundamentals
* Data Lake vs Data Warehouse
* Idempotent pipelines
* Execution date vs system date
* Backfills and reprocessing
* Production-ready logging
* Orchestration design (Airflow-ready)

---

## 🚀 How This Scales in Production

This pipeline can be easily migrated to:

* **Apache Airflow** (DAG with daily schedule)
* **Cloud Storage** (S3 / GCS instead of local files)
* **BigQuery / Snowflake** instead of SQLite
* **dbt** for transformations

---

## 👤 Author

**Julián Silvera**
Data / Analytics Engineer

---

## ✅ Status

✔️ Project completed
✔️ End‑to‑end automated pipeline
✔️ Ready for portfolio & interviews
