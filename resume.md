# Data Engineer Associate Resume

## Data Engineer Tasks and Components

- A data engineer builds data pipelines to enable data-driven decisions.
- Data engineering tasks evolve around ingesting, transforming, and storing data.
- **Replication and migration services** onboard your data into Google Cloud:
  - `gcloud storage`, Storage Transfer Service, Transfer Appliance, Datastream.
- **Data sources** are the origin point of your raw data on Google Cloud:
  - **Ingest**: Cloud Storage, Spanner, Pub/Sub.
- **Transformation services** add new value to your data:
  - Dataflow, Dataform, Dataproc.
- **Data sinks** store your processed data on Google Cloud:
  - Analytics Hub, Dataplex, Bigtable, BigQuery.
- **Cloud Storage** holds your unstructured data:
  1. **Standard storage**: Hot data.
  2. **Nearline storage**: Once per month.
  3. **Coldline storage**: Once every 90 days.
  4. **Archive storage**: Once a year.
- **Options for storing structured data**:
  1. **Transactional workload**:
     - SQL: Cloud SQL (local or regional scalability), Alloy DB (high PostgreSQL scalability), Spanner (global scalability).
     - NoSQL: Firestore.
  2. **Analytical workload**:
     - SQL: BigQuery.
     - NoSQL: Bigtable.
- **Data lake versus data warehouse**:
  1. **Data lake**: Native (unstructured, semi-structured, structured), Cloud Storage.
  2. **Data warehouse**: Schema (structured or semi-structured), BigQuery.
- BigQuery is a serverless, fully managed data warehouse.
- Centrally discover, manage, monitor, and govern distributed data with **Dataplex**:
  - Group and share your data based on readiness.
- Sharing data across organizations with **Analytics Hub** is easy.

## Data Replication and Migration

- Common replication and migration scenarios for ingesting your data into Google Cloud:
  - On-premises, multicloud → BigQuery/Cloud Storage.
- Additional options for migrating your workloads:
  - On-premises, multicloud → BigQuery/AlloyDB/Cloud SQL.
- Choosing between migration options depends on your data volume and network bandwidth:
  - **Small to large data**: `gcloud storage` → Storage Transfer Service → Transfer Appliance.
- Use **Datastream** for continuous RDBMS replication into Google Cloud for analytics:
  - **Use cases**:
    1. Analytics with database replication into BigQuery.
    2. Analytics with custom data processing in Dataflow into BigQuery.
    3. Event-driven architecture.
  - Example: Database replication and migration using Dataflow templates:
    - Source systems → CDC replication (Datastream) → Normalized data (Cloud Storage) → Stream processing (Dataflow) → Database (Spanner).

## Data Pipeline Patterns

### Extract and Load (EL)

- Ingest data into BigQuery without transformation:
  - `bq load`, Data Transfer Service, External tables (BigLake).
- **Three ways of analyzing structured data in BigQuery**:
  1. Load data into BigQuery storage for high performance (requires data movement).
  2. Skip storage for low performance (no data movement required).
  3. Skip storage for high performance (no data movement required).
- **BigLake** uses metadata caching for performance acceleration:
  - Compare **external tables** vs **BigLake tables**.

### Extract, Load, and Transform (ELT)

- Transform data after staging in BigQuery using:
  - Dataform, Jupyter Notebooks, Scheduled queries, Procedural language.
- Dataform simplifies ELT pipeline development and automation:
  - Staging tables → SQL transformation → Production tables.
- SQL workflows can be scheduled and executed with:
  - Dataform, Cloud Scheduler, Cloud Composer.

### Extract, Transform, and Load (ETL)

- Adjust or transform data before loading into BigQuery:
  - Tools: Dataprep, Data Fusion, Dataproc, Dataflow.
- For streaming ETL workloads:
  - Event data → Pub/Sub → Dataflow → BigQuery/Bigtable.

## Automation Techniques

- Automate ELT/ETL workloads:
  - Recurring schedules: Cloud Scheduler, Cloud Composer.
  - Event-driven execution: Cloud Run functions, Eventarc.
- Compare automation options:
  1. Cloud Scheduler: Schedule (YAML).
  2. Cloud Composer: Python workflows.
  3. Cloud Run functions: Events (Python, Java, Go, Node.js, etc.).
  4. Eventarc: Any event source.

## Data Migration Tools

- BigQuery Migration Service:
  1. **Assessment**: BigQuery Migration Assessment Service.
  2. **Data Migration**: BigQuery Data Transfer Service.
  3. **Data Validation**: Data Validation Tool (DVT).
  4. **SQL Translation & Validation**: BigQuery Translation Service.
- Common tools:
  - BigQuery Data Transfer Service (BQDTS): Automated tool.
  - Data Validation Tool (DVT): Open-source CLI.
  - Batch SQL Translator: Converts other SQL dialects into GoogleSQL.
