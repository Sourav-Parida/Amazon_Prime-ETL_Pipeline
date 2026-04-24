# 🚀 Azure Databricks-Based ETL Pipeline with Medallion Architecture (Amazon Prime Dataset)

## 📌 Project Overview
This project demonstrates an end-to-end data engineering pipeline built using Azure services. The pipeline ingests raw data from a GitHub source, processes it through multiple layers using Databricks, and delivers curated data for visualization in Power BI.

The architecture follows the **Medallion Architecture (Bronze → Silver → Gold)** to ensure scalability, data quality, and performance.

---

## 🏗️ Architecture
![Architecture](screenshots/architecture.png)

**Data Flow:**  
GitHub → Azure Data Factory → ADLS Gen2 (Bronze) → Azure Databricks → ADLS (Silver & Gold) → Power BI

---

## ⚙️ Tech Stack
- Azure Data Factory (ADF)  
- Azure Data Lake Storage Gen2 (ADLS)  
- Azure Databricks (PySpark)  
- Delta Lake  
- Power BI  

---

## 🔄 Pipeline Workflow

### 1. Data Ingestion (Bronze Layer)
- Data is extracted from a GitHub repository using ADF  
- ADF Copy Activity loads raw data into ADLS Gen2 (Bronze layer)  
- Data is stored in its original format without transformation  

---

## 🔧 How Azure Data Factory (ADF) Works

![ADF Pipeline](screenshots/adf-pipeline.png)

Azure Data Factory acts as the **orchestration layer** responsible for moving data from the source to the destination.

### 🔹 Key Components Used:

#### 1. Linked Services
- Define connections to external systems  
- Configured for:
  - GitHub (HTTP source)  
  - ADLS Gen2 (destination)  

#### 2. Datasets
- Represent the structure and location of data  
- Define:
  - File format (CSV)  
  - File path (Bronze layer in ADLS)  

#### 3. Pipeline
- Logical container for activities  
- Orchestrates the complete data flow  

#### 4. Copy Activity
- Core component used to transfer data  
- Moves data from GitHub → ADLS Bronze layer  
- Handles schema mapping and file format  

#### 5. Trigger & Debug
- **Debug Mode:** Used for testing pipeline execution  
- **Trigger Now / Schedule Trigger:** Used for production runs  

### 🔹 Execution Flow:
1. ADF connects to GitHub using Linked Service  
2. Reads dataset via defined source dataset  
3. Executes Copy Activity  
4. Writes data into ADLS Bronze layer  

---

### 2. Data Transformation (Silver Layer)
- Azure Databricks is used to clean and transform data  
- Operations performed:
  - Handling missing values  
  - Removing duplicates  
  - Standardizing schema  
- Cleaned data is stored in the Silver layer  

---

### 3. Data Aggregation (Gold Layer)
- Business-level transformations and aggregations are applied  
- Data is stored in Delta format for:
  - ACID transactions  
  - Version control  
  - Faster query performance  
- Final datasets are optimized for analytics and reporting  

---

## 📊 Power BI Dashboard
![Power BI](screenshots/powerbi-dashboard.png)

- Built interactive dashboards to analyze:
  - Genre distribution  
  - Content ratings  
  - Release trends  
- Connected Power BI to Databricks (Gold layer)  

---

## 📁 Project Structure

AMAZON_PRIME-ETL-Pipeline/
│
├── README.md
├── architecture-diagram.png
├── adf-pipeline-json/
│ ├── pipeline_copy_github_to_adls.json
│ ├── linkedservice_github.json
│ ├── linkedservice_adls.json
│ ├── dataset_source.json
│ └── dataset_sink.json
│
├── databricks-notebooks/
│ ├── bronze_to_silver.py
│ └── silver_to_gold.py
│
├── screenshots/
│ ├── architecture.png
│ ├── adf-pipeline.png
│ ├── adf-success.png
│ ├── adls-bronze.png
│ ├── adls-silver.png
│ ├── adls-gold.png
│ ├── databricks.png
│ └── powerbi-dashboard.png
│
└── sample-data/



---

## 🔹 ADF Pipeline Execution
![ADF Run](screenshots/adf-success.png)

- Pipeline successfully executed using Debug and Trigger  
- Data ingested into Bronze layer  
- Monitoring done via ADF Monitor tab  

---

## 🔹 Databricks Transformation
![Databricks](screenshots/databricks.png)

- Implemented PySpark-based transformations  
- Processed data across Bronze → Silver → Gold layers  
- Stored final output using Delta Lake  

---

## 🔹 ADLS Medallion Layers
![ADLS](screenshots/adls-bronze.png)

- **Bronze:** Raw data  
- **Silver:** Cleaned data  
- **Gold:** Business-ready data  

---

## 🚀 Key Highlights
- Designed a scalable ETL pipeline using Azure ecosystem  
- Implemented Medallion Architecture for structured data processing  
- Automated ingestion using ADF pipelines  
- Used Databricks for distributed data transformation  
- Delivered business insights using Power BI  

---

## 🔥 Future Improvements
- Implement incremental data loading  
- Add data validation and quality checks  
- Enable CI/CD deployment for pipelines  

---

## 📎 Dataset
- **Amazon Prime Movies and TV Shows Dataset** by Kaigel  
  Source: https://www.kaggle.com/datasets/shivamb/amazon-prime-movies-and-tv-shows

---