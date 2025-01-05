# Azure-AdventureWorks-Data-Analyst

## Objective
Leverage Azure services to construct a data engineering pipeline that extracts, cleans, transforms, and stores the AdventureWorksDW2022 dataset in a target data warehouse or storage system, making it accessible for Power BI or other visualization tools to create dashboards.

---

## 1. Steps to Design the Data Engineering Pipeline

### Data Extraction (Extract):
- Extract data from the source system, such as AdventureWorksDW2022 stored in Azure SQL Database or other databases.
- Use Azure Data Factory (ADF) Copy Activity to extract the data.

### Data Cleaning and Transformation (Transform):
- Use Azure Data Flow or Azure Databricks for data cleaning and transformation.
- Clean dirty data, handle missing values, and perform field transformations.

### Data Loading (Load):
- Load the cleaned data into the target storage system:
  - Azure Data Lake Storage (ADLS Gen2) for large-scale partitioned storage.
  - Azure Synapse Analytics for complex queries and analysis.
  - Azure SQL Database for structured data and small to medium queries.

### Automation and Scheduling:
- Use ADF Triggers for scheduled or event-driven pipeline execution.
- Automate end-to-end data processing.

---

## 2. Technical Architecture of the Data Engineering Pipeline

### Data Flow Architecture
1. **Source Data**:
   - AdventureWorksDW2022 dataset stored in Azure SQL Database or on-premise SQL Server.

2. **Data Pipeline**:
   - Use Azure Data Factory (ADF) to create pipelines:
     - Copy Activity for data extraction.
     - Data Flow or Databricks for transformation.
     - Load data into the target system.

3. **Target Data Storage**:
   - Azure Data Lake: Partitioned storage for processed data, suitable for big data analysis.
   - Azure Synapse Analytics: Provides analytical services (e.g., OLAP) and complex queries.
   - Azure SQL Database: Stores critical business tables for reporting and dashboarding.

4. **Data Visualization**:
   - Use Power BI to connect to the target data source and create dashboards.

---

## 3. Key Technology Choices

| Data Engineering Task   | Azure Service                         |
|--------------------------|---------------------------------------|
| Data Extraction (Extract) | Azure Data Factory (ADF) Copy Activity |
| Data Cleaning and Transformation (Transform) | Azure Data Factory Data Flow or Azure Databricks |
| Data Loading (Load)      | Azure Data Lake Storage (ADLS Gen2), Synapse Analytics |
| Data Storage (Storage)   | Azure SQL Database, Azure Synapse, ADLS Gen2 |
| Automation (Automation)  | ADF Trigger, Logic Apps               |
| Data Visualization       | Power BI                             |

---

## 4. Implementation Recommendations

### Step 1: Prepare the Source Data
- Upload the AdventureWorksDW2022 dataset to Azure SQL Database.
- Use Azure Portal or Azure CLI to create an Azure SQL Database, and import data using SSMS or other tools.

### Step 2: Create the Data Engineering Pipeline
1. **Create Azure Data Factory**:
   - Create ADF in Azure Portal.
   - Design the pipeline to handle ETL tasks.

2. **Extract Data**:
   - Use ADF's Copy Activity:
     - Source dataset: Azure SQL Database.
     - Target dataset: Azure Data Lake Storage or staging tables.

3. **Transform and Clean Data**:
   - Use Mapping Data Flow or Databricks Notebook:
     - Process dimension tables (e.g., DimCustomer, DimProduct).
     - Aggregate and compute data for fact tables (e.g., FactInternetSales).

4. **Load Data**:
   - Write processed data to:
     - Partitioned paths in Azure Data Lake, e.g.:

       ```
       /processed-data/sales/2023-01/
       ```

     - Analytical tables in Azure Synapse, e.g.:
       - `Sales_Performance`: Summary table for sales by region and time.
       - `Customer_Insights`: Analysis table for customer behaviors.

5. **Schedule the Pipeline**:
   - Use ADF Triggers to schedule data updates:
     - Run daily at midnight.
     - Or trigger based on events, such as file arrivals.

---

## 5. Integrating Visualization Dashboards

- Use Power BI to connect to target data storage (Azure Synapse or Data Lake).
- Create dashboards on the following topics:
  - **Sales Performance Analysis**:
    - Show sales trends by region and time.
  - **Customer Segmentation**:
    - Display high-value customers based on RFM models.
  - **Inventory Status**:
    - Showcase inventory turnover rates and low-stock products.

---

## 6. Example Pipeline

### ETL Tasks
1. **Extract Data**:
   - Extract data from AdventureWorksDW2022's `DimProduct` and `FactInternetSales` tables.

2. **Clean Data**:
   - Handle missing and duplicate values.
   - Convert date fields in `FactInternetSales` to a standard date format.

3. **Partition and Store Data**:
   - Partition data by year and month in Azure Data Lake:

     ```
     /data/processed/sales/2023/01/
     ```

4. **Store in Synapse**:
   - Load processed sales data into target tables in Azure Synapse:
     - Table name: `Sales_Analysis`
