# 📘 Azure Data Factory End-to-End ETL Pipeline Project

---

## 📖 Project Overview
This project demonstrates a complete end-to-end ETL data pipeline using Azure Data Factory. It integrates multiple data sources such as on-premises systems and APIs, processes the data through layered architecture (Bronze, Silver, Gold), and stores it in Azure Data Lake for analytics. The project also includes monitoring and alerting using Azure Logic Apps.

---

## 🎯 Objectives
- Design a scalable ETL architecture using Azure Data Factory  
- Ingest data from multiple sources (On-Premises & API)  
- Implement Medallion Architecture (Bronze, Silver, Gold)  
- Perform data transformations using Mapping Data Flows  
- Enable incremental data loading  
- Implement failure alerts using Logic Apps (Gmail)  

---

## 🏗️ Architecture Overview
This project follows the **Medallion Architecture**:

### 🥉 Bronze Layer
- Raw data ingestion from:
  - On-Prem systems  
  - APIs  
- Stored in Data Lake without transformation  

### 🥈 Silver Layer
- Data cleaning and transformation  
- Applied using Mapping Data Flow  

### 🥇 Gold Layer
- Final curated data  
- Ready for reporting and analytics  

---

## 🔄 Pipeline Orchestration (Parent Pipeline)
### 🔍 Explanation
- Central pipeline controlling the entire workflow  
- Executes:
  - On-Prem Ingestion  
  - API Ingestion  
  - SQL to Data Lake (Incremental Load)  
- Integrated with Logic App (Gmail Alert) for failure notification  

---

## 🏢 On-Premise Ingestion Pipeline


### 🔍 Explanation
- Uses Integration Runtime to connect on-prem data  
- Uses ForEach Activity to process multiple files  
- Copies data to Bronze Layer (Data Lake Storage)  

---

## 🌐 API Ingestion Pipeline

### 🔍 Explanation
- Uses Web Activity to call API  
- Uses Copy Activity to store API response  
- Loads raw JSON data into Bronze layer  

---

## 🥉 Bronze Layer Pipeline

### 🔍 Explanation
- Stores raw, unprocessed data  
- No transformations applied  
- Acts as a source for further processing  

---

## 🥈 Silver Layer Pipeline

### 🔍 Explanation
- Executes Mapping Data Flow  
- Performs:
  - Data cleansing  
  - Filtering  
  - Column transformations  
- Converts raw data into structured format  

---

## 🔄 Data Transformation (Data Flow - DataServing)

### 🔍 Explanation
**Data Flow named `DataServing` performs:**

**Transformations:**
- Derived Column  
- Alter Row (Upsert logic)  
- Select & Filter  
- Data Type Casting  

**Tables Processed:**
- DimAirline  
- DimFlight  
- DimPassenger  
- FactBookings  
- DimAirport  

---

## 🥇 Gold Layer Pipeline

### 🔍 Explanation
- Final transformation layer  
- Aggregated and business-ready data  
- Used for reporting/dashboarding  

---

## 🔁 SQL to Data Lake Pipeline

### 🔍 Explanation
- Performs incremental data loading  
- Moves processed data into Data Lake  
- Ensures efficient updates (no full reload)  

---

## 🧩 Core Components

### 🔗 Linked Services
- Azure Data Lake Storage  
- Azure SQL Database  
- HTTP (API connection)  
- On-Premises Integration Runtime  

---

### ⚙️ Integration Runtime
- Used to connect on-prem systems to Azure  
- Enables secure data movement  

---

### 📦 Storage (Containers)
- Bronze Container → Raw data  
- Silver Container → Cleaned data  
- Gold Container → Final data  

---

### 🗂️ Resource Group
- Central container managing all Azure resources  

**Includes:**
- Data Factory  
- Storage Account  
- Logic App  

---

### 🔁 Pipelines
- Parent Pipeline  
- On-Prem Ingestion Pipeline  
- API Ingestion Pipeline  
- Bronze Layer Pipeline  
- Silver Layer Pipeline  
- Gold Layer Pipeline  
- SQL to Data Lake Pipeline  

---

### 🔄 Data Flows
- DataServing (Main transformation flow)  
- API Data Flow  

---

## 🚨 Monitoring & Alerting

### Logic App Integration
- Triggered when pipeline fails  
- Sends Gmail alert notification  

**Benefits:**
- Real-time monitoring  
- Quick issue resolution  

---

## ⚙️ Key Features
- End-to-End ETL Pipeline  
- Medallion Architecture (Bronze-Silver-Gold)  
- Multi-source ingestion (API + On-Prem)  
- Incremental data loading  
- Parameterized pipelines  
- Failure alert system using Logic Apps  
- Scalable and modular design  

---

## 🚀 Skills Demonstrated

### ☁️ Azure Services
- Azure Data Factory  
- Azure Data Lake Storage  
- Azure SQL Database  
- Azure Logic Apps  
- Azure Resource Management  

---

### 💻 Technical Skills
- ETL Pipeline Design  
- Data Engineering  
- Data Transformation (Mapping Data Flow)  
- Incremental Data Loading  
- API Integration  
- On-Prem Data Integration  
- Workflow Orchestration  

---

### 🧑‍💻 Programming & Query Languages
- SQL  
- Python (if used)  
- JSON  

---

### 📊 Data Concepts
- Medallion Architecture  
- Data Modeling (Fact & Dimension Tables)  
- Data Cleaning & Transformation  
- Data Pipeline Optimization  

---

## 🚧 Challenges Faced

### 🔗 1. On-Premises Linked Service Configuration Issues
**Challenges:**
- Faced difficulty in establishing connection between Azure Data Factory and on-premises system  
- Integration Runtime was not properly configured or not in running state  
- Authentication and permission issues while accessing local data sources  
- Network/firewall restrictions blocking communication between Azure and on-prem environment  

**Solution:**
- Installed and configured Self-Hosted Integration Runtime correctly  
- Ensured Integration Runtime was online and linked to Azure Data Factory  
- Verified credentials and access permissions  
- Allowed required ports and configured firewall settings  

---

### 🔄 2. Integration Runtime Connectivity Issues
**Challenges:**
- Integration Runtime going offline frequently  
- Delays in data movement due to network latency  

**Solution:**
- Restarted and monitored Integration Runtime service  
- Ensured stable internet connection  
- Optimized pipeline execution timing  

---

### ⚙️ 3. Data Flow Debugging Issues
**Challenges:**
- Debug session taking too long to start (10+ minutes)  
- Unable to preview data in Data Flow  
- Cluster initialization delays  

**Solution:**
- Enabled Data Flow Debug mode properly  
- Selected appropriate compute size for faster execution  
- Waited for cluster warm-up or reused active debug session  

---

### 🔍 4. Data Preview Not Showing
**Challenges:**
- Data preview not visible in transformations like Alter Row  
- Schema mismatch errors  

**Solution:**
- Refreshed dataset schema  
- Validated source data and column mappings  
- Ensured debug mode was active before preview  

---

### 🔁 5. Alter Row (Upsert) Issues
**Challenges:**
- All rows marked incorrectly (e.g., all showing same rank/value)  
- Upsert conditions not working as expected  

**Solution:**
- Corrected conditional expressions in Alter Row  
- Verified key columns for upsert logic  
- Tested logic with sample data  

---

### ⏱️ 6. Pipeline Debug Performance Issues
**Challenges:**
- Debug execution taking longer time  
- Increased cost due to long debug sessions  

**Solution:**
- Used debug mode only when required  
- Stopped debug session after testing  
- Optimized transformations and pipeline design  

---
# 🖼️ Screenshots & Implementation

## 🔹 1. Parent Pipeline (Orchestration)
<img width="940" height="531" alt="image" src="https://github.com/user-attachments/assets/d77d2baf-2578-426e-afe4-ca023a561535" />


**Description:**
- Main orchestration pipeline controlling all workflows  
- Executes ingestion, transformation, and loading pipelines  
- Includes failure alert mechanism using Logic App  

---

## 🔹 2. On-Premise Ingestion Pipeline
<img width="940" height="528" alt="image" src="https://github.com/user-attachments/assets/120c5afb-4006-476e-b33c-5882a6e2d099" />


**Description:**
- Uses Integration Runtime to connect on-premises systems  
- Processes multiple files using ForEach activity  
- Loads raw data into Bronze layer  

---

## 🔹 3. API Ingestion Pipeline
<img width="940" height="494" alt="image" src="https://github.com/user-attachments/assets/d157fb3e-5e23-4b48-b5b8-6cc06f85509f" />


**Description:**
- Calls external API using Web Activity  
- Stores response using Copy Activity  
- Loads JSON data into Data Lake  

---

## 🔹 4. Bronze Layer
<img width="940" height="531" alt="image" src="https://github.com/user-attachments/assets/8a6520f1-b492-4d54-889f-e1b19aaaf3f7" />


**Description:**
- Stores raw and unprocessed data  
- Acts as the initial data ingestion layer  

---

## 🔹 5. Silver Layer Pipeline
<img width="940" height="499" alt="image" src="https://github.com/user-attachments/assets/3ca11814-dafd-42ec-b0b0-af13b69b5852" />


**Description:**
- Executes Mapping Data Flow  
- Performs data cleaning and transformation  

---

## 🔹 6. Data Flow (Transformation - DataTransformation and DataServing for Gold Layer)
<img width="940" height="421" alt="image" src="https://github.com/user-attachments/assets/8381042d-edff-4d6c-9ef1-31c20ebd627d" />


**Description:**
- Applies transformations like Derived Column, Filter, Alter Row  
- Converts raw data into structured format  
- Handles multiple datasets (Dim & Fact tables)  

---

## 🔹 7. Gold Layer Pipeline
<img width="940" height="528" alt="image" src="https://github.com/user-attachments/assets/fb0c9ccd-3e6b-4f2c-83b9-04d9d943ff41" />


**Description:**
- Final transformed and aggregated data  
- Ready for reporting and analytics  

---

## 🔹 8. SQL to Data Lake Pipeline
<img width="940" height="528" alt="image" src="https://github.com/user-attachments/assets/ebaa7125-dc3d-4681-aa2a-cf62cdcbfff4" />


**Description:**
- Performs incremental data loading  
- Moves processed data into Data Lake  

---

## 🔹 9. Linked Services Configuration
<img width="940" height="528" alt="image" src="https://github.com/user-attachments/assets/76092af0-565f-424e-83b4-ee3cd1c3f032" />


**Description:**
- Configurations for:
  - Azure Data Lake Storage  
  - Azure SQL Database  
  - API (HTTP)  
  - On-Prem Integration Runtime  

---

## 🔹 10. Integration Runtime
<img width="940" height="528" alt="image" src="https://github.com/user-attachments/assets/f605da07-7a36-4c33-8667-de01192fc8f5" />


**Description:**
- Enables secure data transfer between on-prem and Azure  
- Required for hybrid data integration  

---

## 🔹 11. Storage Containers
<img width="940" height="528" alt="image" src="https://github.com/user-attachments/assets/0ed3fe43-ca18-475f-9f9e-4e0253a46b65" />


**Description:**
- Bronze → Raw data  
- Silver → Cleaned data  
- Gold → Final data  

---

## 🔹 12. Logic App (Failure Alert - Gmail)
<img width="940" height="497" alt="image" src="https://github.com/user-attachments/assets/1045742c-c903-4c22-8c85-492b4ad8bad5" />


**Description:**
- Sends email alerts when pipeline fails  
- Helps in real-time monitoring and debugging  

---
---

## 📊 Results
- Successfully built a scalable ETL pipeline  
- Integrated multiple data sources  
- Delivered analytics-ready datasets  

---

## 🔮 Future Enhancements
- CI/CD pipeline integration  
- Real-time streaming data  
- Dashboard integration (Power BI)  
- Advanced monitoring  

---

## 🙋‍♀️ Author
**Madhavi Prabhakar Thakare**
