# 🚗 Car Sales Data Engineering Pipeline on Azure

This project demonstrates an end-to-end **data engineering pipeline** for ingesting, transforming, and serving car sales data using the Azure ecosystem and Databricks, following a Medallion Architecture (Bronze → Silver → Gold). It supports **incremental loading**, **SCD Type 1** logic, and is built for real-world scalability.

![Architecture](./de1.jpg)

## 🔧 Tech Stack

- **Azure Data Factory** – Data orchestration
- **Azure SQL Database** – Staging & checkpointing
- **Azure Data Lake Storage (ADLS Gen2)** – Bronze, Silver, Gold layers
- **Azure Databricks** – Data transformation and pipeline orchestration
- **GitHub** – Source control and raw data hosting
- **Power BI** – Reporting & dashboarding
- **Azure Synapse** – Analytics integration
- **Unity Catalog** – Data governance

---

## 🚀 Pipeline Overview

### 🔹 Step 1: Data Ingestion
- Raw car sales data (`.csv`) is stored in [GitHub](https://github.com/Nagarjun-CS/Car_Sales_DE).
- **ADF Pipeline 1**:
  - Takes file name as a parameter.
  - Loads data from GitHub → Azure SQL Table.
  
### 🔹 Step 2: Incremental Load & Checkpointing
- **Checkpoint Table** tracks the last successful data load date.
- **ADF Pipeline 2**:
  - Fetches the checkpoint date.
  - Loads only **new data** from Azure SQL → ADLS (Bronze Layer) in Parquet format.
  - Updates the checkpoint table using a stored procedure.

![Incremental Load Flow](./26ffc0bf-bac5-4512-a082-995cf51c9070.png)

---

## 🪄 Data Transformation with Databricks

### 🔸 Silver Layer
- Cleaned and formatted data.
- New columns derived from raw data.
- Stored as Parquet in Silver zone (ADLS).

### 🔸 Gold Layer
- Implemented **Star Schema** with dimension and fact tables.
- Applied **SCD Type 1** logic for slowly changing dimensions.
- Stored in Gold zone (ADLS) in Parquet format.

### 🔸 Orchestration
- Notebooks developed for:
  - Silver transformations.
  - Gold layer dimension & fact tables (parallelized).
- Scheduled using **Databricks Jobs & Pipelines**.

---

## 📊 Reporting & Analysis

- **Power BI**: Final gold layer data used for interactive dashboards.
- **Azure Synapse**: Connected for advanced analytics and queries.

---

## 📁 Project Structure

