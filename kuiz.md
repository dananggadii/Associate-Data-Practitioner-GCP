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

# Data Pipeline and AI Concepts in Google Cloud

## The Extract, Load, and Transform (ELT) Data Pipeline Pattern

### Questions and Answers

1. **What is the primary purpose of assertions in Dataform?**

   - **Answer**: To define data quality tests, ensuring data consistency and accuracy.

2. **How does Dataform enhance the management of SQL workflows in BigQuery?**

   - **Answer**: It unifies transformation, assertion, and automation within BigQuery, streamlining data operations.

3. **Which of the following best describes the core concept of extract, load, and transform (ELT)?**

   - **Answer**: Loading data into a data warehouse and then transforming it within the warehouse.

4. **Which of the following is a key benefit of using stored procedures in BigQuery?**

   - **Answer**: The improvement of code reusability and maintainability.

5. **What is the primary advantage of using BigQuery's procedural language support?**
   - **Answer**: It enables the execution of multiple SQL statements in sequence with shared state.

---

## The Extract, Transform, and Load (ETL) Data Pipeline Pattern

### Questions and Answers

1. **Which Google Cloud service is specifically designed for serverless, no-code data transformation using recipes?**

   - **Answer**: Dataprep.

2. **Which Google Cloud service is best suited for building complex data pipelines with a visual, drag-and-drop interface?**

   - **Answer**: Data Fusion.

3. **What is the primary advantage of using Dataflow templates?**

   - **Answer**: It allows for reusability and parameterization of pipelines.

4. **Which Google Cloud service is recommended for handling streaming data pipelines that require millisecond-level latency analytics?**

   - **Answer**: Bigtable.

5. **Which of the following features makes Dataproc Serverless for Spark ideal for interactive development and exploration?**
   - **Answer**: JupyterLab integration.

---

## Automation Techniques

### Questions and Answers

1. **In the context of Cloud Composer, what is a DAG?**

   - **Answer**: Directed acyclic graph.

2. **Which Google Cloud service acts as a central orchestrator, seamlessly integrating your pipelines across diverse systems?**

   - **Answer**: Cloud Composer.

3. **Which of the following Google Cloud services allows you to execute code in response to various Google Cloud events?**

   - **Answer**: Cloud Run functions.

4. **Which of the following Google Cloud services allows you to automate tasks by invoking your workloads at specified, recurring intervals?**

   - **Answer**: Cloud Scheduler.

5. **Which of the following services enables the creation of a unified event-driven architecture for loosely coupled services?**
   - **Answer**: Eventarc.

---

## AI Foundations

### Questions and Answers

1. **If you have unstructured data, like images, text, and/or audio, which storage option on Google Cloud would you choose?**

   - **Answer**: Cloud Storage.

2. **Which Google hardware innovation tailors architecture to meet the computation needs on a domain, such as the matrix multiplication in machine learning?**

   - **Answer**: TPUs (tensor processing units).

3. **Vertex AI, AutoML, and Generative AI Studio align to which stage of the data-to-AI workflow?**

   - **Answer**: Machine learning.

4. **Which of the following is one of Google’s seven principles for responsible AI?**

   - **Answer**: AI should avoid creating or reinforcing unfair bias.

5. **What are the three layers of the AI/ML framework on Google Cloud?**

   - **Answer**: AI foundations, AI development, and AI solutions.

6. **Which SQL command would you use to create an ML model in BigQuery ML?**

   - **Answer**: CREATE MODEL.

7. **You want to use machine learning to discover the underlying pattern and group a collection of unlabeled photos into different sets. Which should you use?**

   - **Answer**: Unsupervised learning, cluster analysis.

8. **On Cloud Storage, which data storage class is best for storing data that needs to be accessed less than once a year?**
   - **Answer**: Archive storage.

---

## AI Development Options

### Questions and Answers

1. **You want to predict guest trends in BigQuery using SQL and ML. What is the best option?**

   - **Answer**: BigQuery ML.

2. **You need a codeless solution for training your own machine learning model. What do you use?**

   - **Answer**: AutoML.

3. **Which code-based solution gives data scientists full control over ML development?**

   - **Answer**: Custom training.

4. **Which of the following can you do with the Natural Language API?**

   - **Answer**: Analyze sentiment and identify subjects of text.

5. **Which of the following lets you create a neural network with multiple layers?**

   - **Answer**: tf.keras.Sequential.

6. **A video company wants to categorize event footage but doesn't want to train an ML model. What should they use?**
   - **Answer**: Pre-trained APIs.

---

## AI Development Workflow

### Questions and Answers

1. **What is the key metric for detecting defective apples without wasting good ones?**

   - **Answer**: Precision.

2. **Select the correct machine learning workflow.**

   - **Answer**: Data preparation, model development, model serving.

3. **Which stage includes data upload and feature engineering?**

   - **Answer**: Data preparation.

4. **What is the key metric for identifying as many cancer cases as possible?**

   - **Answer**: Recall.

5. **Which tool automates, monitors, and governs ML workflows in a serverless manner?**

   - **Answer**: Vertex AI Pipelines.

6. **When building an ML pipeline on Vertex AI, what components can you use?**

   - **Answer**: Both prebuilt and custom components.

7. **Which stage includes model training and evaluation?**
   - **Answer**: Model development.

---

## Generative AI

### Questions and Answers

1. **What is a few-shot prompt?**

   - **Answer**: A type of prompt that allows a model to perform tasks with a small number of examples.

2. **What is Vertex AI Studio?**

   - **Answer**: A tool for testing and customizing generative AI models for applications.

3. **How does generative AI generate new content?**

   - **Answer**: It learns from massive existing content and can solve specific problems after further tuning.

4. **What is a prompt?**

   - **Answer**: A natural language request or instruction to guide a model to generate a desired output.

5. **What AI solution should a call center use for improving efficiency and automating routine requests?**

   - **Answer**: Contact Center AI.

6. **What are the two categories of AI solutions by Google Cloud?**

   - **Answer**: Vertical solutions and horizontal solutions.

7. **How can you generate more creative content in Generative AI Studio?**
   - **Answer**: Set the temperature to a high value.
