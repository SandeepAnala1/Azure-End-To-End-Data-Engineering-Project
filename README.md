## Azure End-To-End Data Engineering Project

### 📌 Project Overview

In this project, I built a **production-grade end-to-end data engineering solution on Azure**, following modern data engineering practices. The primary goal was to gain hands-on experience with tools and techniques that are in demand for Azure data engineering roles. I implemented the **Medallion architecture** and focused on key aspects such as **incremental data loading**, **star schema modeling**, and **handling slowly changing dimensions (SCDs)**. This project enabled me to simulate real-world data pipeline development and deployment, preparing me for enterprise-level data engineering responsibilities.

---

### 🛠️ Tools & Technologies Used

- **Azure Data Lake Storage Gen2 (ADLS):** Used for storing data across Bronze, Silver, and Gold layers.
- **Azure SQL Database:** Served as the source system for transactional data.
- **Azure Data Factory (ADF):** Used for orchestrating ETL pipelines and enabling incremental data loading through **Change Data Capture (CDC)** and **lookup activities**.
- **Azure Databricks:** Utilized for data transformation, star schema modeling, and SCD implementation using **PySpark**.
- **Unity Catalog:** Managed data governance, access control, and organization of tables and schemas in Databricks.
- **Delta Lake:** Enabled ACID-compliant data storage with versioning and time travel for Silver and Gold layers.
- **PySpark & SQL:** Used extensively within Databricks notebooks for transformations and data modeling.
- **GitHub:** Hosted the initial dataset in CSV format.
- **Power BI:** Used for data visualization and dashboarding from the Gold (serving) layer.
- **HTTP Connector (ADF):** Used to retrieve data files from GitHub.
- **Azure CLI:** Used to provision necessary cloud resources where applicable.

---

### 🏗️ Architecture

The pipeline adheres to the **Medallion Architecture**, structured into three layers:
![image](https://github.com/user-attachments/assets/641de7fe-72d5-4668-a7d7-e65be9e433b2)

#### 1. Bronze Layer (Raw)
- Ingested raw data from **Azure SQL Database** to **ADLS** in CSV format.
- Enabled **incremental loading** to fetch only new or changed records.

#### 2. Silver Layer (Transformed)
- Cleaned and transformed the raw data using **Azure Databricks**.
- Calculated new features such as **Revenue per Unit**.
- Converted datasets into **Delta format** for performance and reliability.

#### 3. Gold Layer (Serving)
- Built a **star schema** with **fact and dimension tables** in Databricks.
- Applied **SCD Type 1** logic for dimension updates using PySpark.
- Stored the modeled data in **Delta format** on ADLS for downstream analytics.

![image](https://github.com/SandeepAnala1/Azure-End-To-End-Data-Engineering-Project/blob/main/images/AzureDataLake%20Containers.png)
---

### 🔄 Pipeline Implementation

#### 1. Data Sources
- **Azure SQL Database**: Hosted the core transactional data.
- **GitHub**: Provided the initial and incremental datasets in CSV format.

#### 2. Ingestion
- Used **ADF Copy Activity** to perform the initial load from GitHub to Azure SQL Database.
- Implemented **incremental loading** using:
  - ADF Lookup Activities
  - **Watermark Table** in SQL DB
  - Stored Procedures for updating watermark logic
  - Parameterized SQL queries to fetch only new data

![image](https://github.com/SandeepAnala1/Azure-End-To-End-Data-Engineering-Project/blob/main/images/Pipelines/Incremental%20Pipeline/Azure%20Data%20Factory%20Incremental%20Pipeline.png)

#### 3. Transformation (Databricks)
- **Bronze to Silver**:
  - Loaded data from ADLS (CSV/Parquet)
  - Cleaned, engineered features using PySpark
  - Wrote data in **Delta format**

- **Silver to Gold**:
  - Designed and implemented the **dimensional model**
  - Created **Surrogate Keys** and **joined** dimension tables to fact table
  - Applied **SCD Type 1 (Upsert)** logic for maintaining current dimension values
  - Outputted the modeled data to the Gold layer in Delta format

#### 4. Storage
- All layers (Bronze, Silver, Gold) stored in **Azure Data Lake Gen2**
- **Delta format** used for Silver and Gold layers to ensure scalable, version-controlled storage

#### 5. Orchestration
- **ADF Pipelines**: Orchestrated data loading from SQL DB to Bronze layer
- **Databricks Jobs/Workflows**: Chained notebook executions for transformation from Silver to Gold
- **ADF** optionally used to trigger Databricks jobs

#### 6. Data Consumption
- The **Gold layer** acts as the serving layer for analytics
- Connected **Power BI** to visualize insights and dashboards
- Queried Gold data using **Databricks SQL Editor** for exploratory analysis

---

### 📊 Key Results

- Successfully delivered a **fully functional data pipeline** from ingestion to modeling
- Implemented **incremental loading**, improving resource usage and processing efficiency
- Built a **star schema** optimised for analytical querying and BI reporting
![image](https://github.com/SandeepAnala1/Azure-End-To-End-Data-Engineering-Project/blob/main/images/Databricks/Databricks_Data%20Model_Workflow.png)

- Implemented **Slowly Changing Dimensions (SCD Type 1)** for maintaining accurate and up-to-date dimensions
- Leveraged **Unity Catalog** for structured data governance and access control
- Enabled BI connectivity through **Power BI**, ready for enterprise reporting use cases

---

### ✅ Conclusion

This project gave me end-to-end exposure to building a modern cloud-based data pipeline using the **Azure ecosystem**. By applying the **Medallion architecture**, I ensured clean separation of concerns across raw, cleaned, and analytical layers. The use of **incremental loads**, **star schema modeling**, and **SCD handling** reflects industry standards in data warehousing and engineering. Through this implementation, I demonstrated a scalable and modular approach to data engineering, making me job-ready for Azure data engineering roles.

---

