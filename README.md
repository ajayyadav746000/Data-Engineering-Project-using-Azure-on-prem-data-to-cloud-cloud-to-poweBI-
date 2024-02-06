# Data-Engineering-Project-using-Azure-on-prem-data-to-cloud-cloud-to-poweBI-

## Project Overview:
 Data engineering project on Azure that involved moving data from on-premise SQL Server to Azure Data Lake through Data Factory. 
 Using Databricks and Spark, I transformed the data before loading it into Synapse. 
 The final step included setting up PowerBI for reporting, providing stakeholders with valuable insights.


## Dataset:
 The AdventureWorks database, freely available online and provided by Microsoft, serves as a sample database to illustrate the design of a SQL server database, originally demonstrated with SQL Server 2008. It showcases the structure of a database supporting a fictional manufacturing multinational corporation named Adventure Works Cycles.

This database is specifically designed for Online Transaction Processing (OLTP), a type of data processing involving concurrent transactions. Microsoft ships the AdventureWorks database with their SQL server products.

In the context of this project, I utilized the Lightweight (LT) data, a streamlined version of the OLTP sample, to ensure efficiency and simplicity. You can download the LT data here.

Please find the relevant data in the :https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorksLT2017.bak

## Project Objectives:

1. Establish a connection between an on-premise SQL server and Azure cloud.
2. Ingest tables into Azure Data Lake for efficient storage and accessibility.
3. Apply data cleaning and transformation processes using Azure Databricks.
4. Utilize Azure Synapse Analytics to load the cleaned data for further analysis.
5. Create interactive data visualizations and reports using Microsoft Power BI for effective insights.
6. Implement Azure Active Directory (AAD) and Azure Key Vault for robust monitoring and governance of the data pipeline.

These goals outline the key steps in setting up a comprehensive data engineering project on the Azure cloud.

##  Project Architecture:

![Alt Text](https://github.com/ajayyadav746000/Data-Engineering-Project-using-Azure-on-prem-data-to-cloud-cloud-to-poweBI-/blob/main/Screenshot%202023-10-11%20225825.png)


## 1: Data Ingestion

To facilitate data ingestion from the on-premises SQL server to Azure SQL, the process is executed through Azure Data Factory. The key steps involve:

1. Installation of Self-Hosted Integration Runtime.
2. Establishing a secure connection between Azure Data Factory and the on-premises SQL Server.
3. Configuration of a copy pipeline designed to transfer all tables seamlessly from the local SQL server to the designated "bronze" folder within Azure Data Lake.

These steps ensure a systematic and secure transfer of data, setting the foundation for downstream processing and analysis in the Azure cloud environment.

## 2: Data Transformation

Following the data ingestion into the "bronze" folder, a structured transformation process is implemented based on the medallion data lake architecture (bronze, silver, gold). This multi-layered approach ensures the data is refined progressively, making it optimal for utilization in business reporting tools like Power BI.

Azure Databricks, leveraging PySpark, plays a pivotal role in executing these transformations. The initial data, stored in parquet format within the "bronze" folder, undergoes a conversion to the delta format as it advances through the "silver" and "gold" layers. This transformation is orchestrated through Databricks notebooks, encompassing the following steps:

1. Mounting the storage.
2. Transforming the data from the "bronze" layer to the "silver" layer.
3. Further enhancing the data from the "silver" layer to the refined "gold" layer.

This staged transformation ensures data quality and structure, setting the stage for meaningful insights and streamlined reporting in downstream processes.

## 3: Data Loading

The data residing in the "gold" folder undergoes loading into the Business Intelligence reporting application, Power BI, facilitated by Azure Synapse. The loading process unfolds through the following steps:

1. Establishing a connection between Azure Storage (Gold Folder) and Azure Synapse.
2. Crafting stored procedures responsible for extracting table information and presenting it as a SQL view.
3. Storing these views within a server-less SQL Database in Synapse.

This systematic approach ensures a seamless transition of refined data from the gold layer to Azure Synapse, providing a foundation for efficient querying and reporting in Power BI.

## 4: Data Reporting

Power BI establishes a direct connection to the cloud pipeline utilizing DirectQuery for real-time database updates. The development of a Power BI report unfolds to visualize the AdventureWorks dataset, encompassing key aspects such as sales, product information, and customer gender. This approach ensures dynamic and up-to-date reporting, enhancing the accessibility and insights derived from the AdventureWorks data within Power BI.


## 5: Final Pipeline Test

To validate the integrity of the end-to-end pipeline, the addition of two new customers to the local SQL database server is initiated. A successful execution of this process triggers the pipeline to update, and the Power BI report dynamically reflects the inclusion of the new data. The expected outcome is an increase in the total number of customers from 847 to 849, serving as a conclusive test of the entire data pipeline's functionality.



## Conclusion and Considerations:

This project showcases the successful development of a comprehensive end-to-end ETL cloud solution utilizing Azure. Several considerations and limitations are noted:

1. **Dataset Size:**
   - The project utilized a relatively small dataset (7MB total, 800 rows) to mitigate compute and storage costs. This decision was made to optimize personal expenses during the project.

2. **Tool Diversity:**
   - Multiple applications were employed for what could be considered a relatively simple task. In retrospect, given the simplicity of the dataset, the project could have been effectively managed using Azure Data Factory alone, with data cleaning carried out downstream in Power BI.

3. **Alternative Approaches:**
   - Considering the straightforward nature of the dataset, it could have been feasible to streamline the project, relying solely on Azure Data Factory for end-to-end management. This would involve moving data cleaning processes to Power BI, simplifying the overall solution.

4. **Learning and Emulation:**
   - The inclusion of Azure Synapse and Databricks in the project was primarily for the purpose of self-learning and emulating real-world business pipelines. While these tools added complexity, they provided valuable insights into broader Azure capabilities.

In conclusion, while acknowledging these considerations, the project successfully demonstrates the construction of a functional ETL pipeline on Azure, highlighting adaptability to varying project scopes and the incorporation of diverse Azure services for educational purposes.
