# Solution Architecture Report

This document provides an overview of the solution architecture for ingesting, transforming, and storing COVID-19 and population data using Azure Data Factory (ADF) and related Azure services. The architecture focuses on data ingestion, transformation, storage, and reporting processes.

## 1. Data Ingestion

The project involves ingesting two primary datasets:

- **COVID-19 Data from ECDC (European Center for Disease Prevention and Control)**: This data is accessed via the HTTP connector within Azure Data Factory.
  
- **Population Data from Eurostat**: Instead of directly retrieving the data from Eurostat, we store a curated version of it in an Azure Blob Storage account and access it from there. This approach demonstrates the use of an additional type of connector within ADF.

Both datasets are subsequently ingested into **Azure Data Lake Storage Gen 2**.

## 2. Data Transformation

Azure Data Factory is used to transform the data, employing three different transformation tools to illustrate its flexibility:

- **Data Flows in Azure Data Factory**: A code-free transformation tool for simplifying low to medium complexity transformations.
  
- **HDInsight**: Used for more complex transformations, HDInsight allows code-based transformations using languages supported by Spark, such as Python, Scala, and Spark SQL, as well as Hive (a SQL-like language) and Pig scripting.

- **Azure Databricks**: Similar to HDInsight, Databricks supports advanced, code-driven transformations using Spark-based languages.

Data Factory acts as the orchestration tool for HDInsight and Databricks transformations, scheduling and managing these processes rather than directly performing the transformations.

## 3. Data Storage

The following storage solutions are used to organize and store the ingested and transformed data:

- **Azure Blob Storage**: Used for storing the Eurostat population data, allowing centralized data distribution across teams or to external stakeholders.

- **Azure Data Lake Storage Gen 2**: The primary data lake for this project. Azure Data Lake Storage Gen 2 offers high performance, scalability, and enhanced security, making it ideal for enterprise-level data lakes with petabyte-scale storage and high throughput.

- **Azure SQL Database**: A subset of the transformed data is stored in an Azure SQL Database for reporting purposes. Although Azure Synapse Analytics is better suited for large data warehouses, Azure SQL Database is appropriate here due to the smaller data volume.

## 4. Reporting

For reporting, **Power BI** is used to create trend reports based on the data stored in the Azure SQL Database. Although the primary focus of this course is Azure Data Factory, Power BI’s capabilities are leveraged to develop, visualize, and share meaningful insights across teams.

## 5. Technology Selection Rationale

Azure Data Factory was chosen because it provides a broad range of connectors for data integration and orchestrates the workflows for each of the transformation tools. Each transformation tool was chosen to demonstrate specific capabilities:

- **Data Flows** for low-code, simpler transformations.
- **HDInsight and Databricks** for code-driven, complex transformations.

For storage, each solution meets a distinct requirement:

- **Blob Storage** for distributing raw data.
- **Data Lake Gen 2** for scalable, secure data storage.
- **SQL Database** for structured data in reporting.

## Conclusion

This solution architecture demonstrates the effective use of Azure services in data ingestion, transformation, storage, and reporting, tailored to meet the requirements of this project. The flexibility of Azure Data Factory allows for easy future expansion if additional data sources or transformation requirements arise.
