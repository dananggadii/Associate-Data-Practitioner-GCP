# Datastream: PostgreSQL Replication to BigQuery

### Create the Cloud SQL database
1. Run the following command to enable the Cloud SQL API:
```
gcloud services enable sqladmin.googleapis.com
```
![image](https://github.com/user-attachments/assets/1afcb50c-5dc0-46e7-9447-53f9fc9712ca)

![image](https://github.com/user-attachments/assets/c90e984e-2873-4600-afa8-1bc910846d06)

2. Run the following command to create a Cloud SQL for PostgreSQL database instance:
```
POSTGRES_INSTANCE=postgres-db
DATASTREAM_IPS=34.91.152.13,35.204.79.99,34.90.129.65,34.90.22.40,35.204.21.106
gcloud sql instances create ${POSTGRES_INSTANCE} \
    --database-version=POSTGRES_14 \
    --cpu=2 --memory=10GB \
    --authorized-networks=${DATASTREAM_IPS} \
    --region=europe-west4 \
    --root-password pwd \
    --database-flags=cloudsql.logical_decoding=on
```
**Note**: This command creates the database in europe-west4. For other regions, be sure to replace the **DATASTREAM_IPS** with the right [Datastream Public IPs](https://cloud.google.com/datastream/docs/ip-allowlists-and-regions) for your region.

### Populate the database with sample data
1. Connect to the PostgreSQL database by running the following command in Cloud Shell.
```
gcloud sql connect postgres-db --user=postgres
```
   When prompted for the password, enter **pwd**.
   
2. Once connected to the database, run the following SQL command to create a sample schema and table:
```
CREATE SCHEMA IF NOT EXISTS test;

CREATE TABLE IF NOT EXISTS test.example_table (
id  SERIAL PRIMARY KEY,
text_col VARCHAR(50),
int_col INT,
date_col TIMESTAMP
);

ALTER TABLE test.example_table REPLICA IDENTITY DEFAULT; 

INSERT INTO test.example_table (text_col, int_col, date_col) VALUES
('hello', 0, '2020-01-01 00:00:00'),
('goodbye', 1, NULL),
('name', -987, NOW()),
('other', 2786, '2021-01-01 00:00:00');
```

3. 
