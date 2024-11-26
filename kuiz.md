# Data Engineer Quiz

## Data Engineering Tasks and Components

1. **What is the purpose of Analytics Hub in Google Cloud?**

   - a. To provide a centralized platform for data visualization.
   - b. To perform complex machine learning tasks on large datasets.
   - c. To automate the process of data cleaning and transformation.
   - **d. To enable secure and controlled data sharing within and outside an organization.**

2. **What is the key difference between a data lake and a data warehouse?**

   - a. Data lakes are used for real-time analytics, while data warehouses are used for long-term storage.
   - b. Data lakes are managed by data scientists, while data warehouses are managed by data engineers.
   - c. Data lakes store only structured data, while data warehouses store unstructured data.
   - **d. Data lakes store raw, unprocessed data, while data warehouses store processed and organized data.**

3. **Which Google Cloud product is best suited for storing unstructured data like images and videos?**

   - a. BigQuery
   - **b. Cloud Storage**
   - c. Bigtable
   - d. Cloud SQL

4. **Which stage in a data pipeline involves modifying and preparing data for specific downstream requirements?**

   - a. Ingest
   - **b. Transform**
   - c. Replicate and migrate
   - d. Store

5. **What is the primary function of a data engineer?**
   - a. Managing network security for data systems.
   - b. Designing user interfaces for data visualization.
   - **c. Building and maintaining data pipelines.**
   - d. Conducting statistical analysis on data.

---

## Data Replication and Migration

1. **Which tool or service uses the `cp` command to facilitate ad-hoc transfers directly to Cloud Storage from various on-premise sources?**

   - a. Transfer Appliance
   - b. Datastream
   - c. Storage Transfer Service
   - **d. gcloud storage command**

2. **Which of the following services efficiently moves large datasets from on-premises, multicloud file systems, object stores, and HDFS into Cloud Storage and supports scheduled transfers?**

   - a. Vertex AI
   - b. Transfer Appliance
   - **c. Storage Transfer Service**
   - d. gcloud storage

3. **The ease of migrating data is heavily influenced by which two factors?**

   - a. Data source and destination platform
   - b. Data format and storage type
   - **c. Data size and network bandwidth**
   - d. Data complexity and network latency

4. **In Datastream event messages, which section contains the actual data changes in a key-value format?**

   - a. Generic metadata
   - b. Source-specific metadata
   - **c. Payload**
   - d. Change log

5. **Which of the following tools is best suited for migrating very large datasets offline?**
   - a. Storage Transfer Service
   - b. Datastream
   - **c. Transfer Appliance**
   - d. gcloud storage command

---

## The Extract and Load Data Pipeline Pattern

1. **Which of the following statements accurately describes the staleness configuration for BigLake's metadata cache?**

   - **a. The staleness can be configured between 30 minutes to 7 days and can be refreshed automatically or manually.**
   - b. The staleness can be configured between 15 minutes to 1 day.
   - c. The cache is refreshed only manually.
   - d. The staleness cannot be configured and remains fixed.

2. **What is the main advantage of using BigLake tables over external tables in BigQuery?**

   - a. BigLake tables require separate permissions for the table and the data source.
   - b. BigLake tables have strong limitations on data formats and storage locations.
   - c. BigLake tables are simpler to set up.
   - **d. BigLake tables offer enhanced performance, security, and flexibility.**

3. **Which of the following BigQuery features or services allows you to query data directly in Cloud Storage without loading it into BigQuery?**

   - a. The `bq mk` command
   - b. The `bq load` command
   - c. The BigQuery Data Transfer Service
   - **d. External tables**

4. **The `LOAD DATA` statement in BigQuery is best suited for which scenario?**

   - a. Creating a new dataset in BigQuery.
   - b. Loading data from a local CSV file using a graphical interface.
   - **c. Automating data loading into BigQuery tables within a script or application.**
   - d. Querying data directly from Google Sheets without loading it into BigQuery.

5. **Which of the following best describes the BigQuery Data Transfer Service?**
   - **a. It is a fully-managed service for scheduling and automating data transfers into BigQuery from various sources.**
   - b. It is a command-line tool for loading data into BigQuery.
   - c. It is a service that allows querying data directly in Cloud Storage.
   - d. It is a feature that enables querying data across Cloud Storage and other cloud object stores.

---
