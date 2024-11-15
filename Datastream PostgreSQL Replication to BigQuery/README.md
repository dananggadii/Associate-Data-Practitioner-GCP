# Datastream: PostgreSQL Replication to BigQuery

## Create a database for replication
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
![image](https://github.com/user-attachments/assets/262d391c-ca82-4f5e-8a57-3b827508689d)

**Note**: This command creates the database in europe-west4. For other regions, be sure to replace the **DATASTREAM_IPS** with the right [Datastream Public IPs](https://cloud.google.com/datastream/docs/ip-allowlists-and-regions) for your region.

### Populate the database with sample data
1. Connect to the PostgreSQL database by running the following command in Cloud Shell.
```
gcloud sql connect postgres-db --user=postgres
```
When prompted for the password, enter **pwd**.
![image](https://github.com/user-attachments/assets/8fa9dcf8-fe57-4d1a-8ba2-23a92615a5f1)
   
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
![image](https://github.com/user-attachments/assets/5bfc6c80-00b9-4ce5-b24a-75bb46f0b866)

### Configure the database for replication
1. Run the following SQL command to create a publication and a replication slot:
```
CREATE PUBLICATION test_publication FOR ALL TABLES;
ALTER USER POSTGRES WITH REPLICATION;
SELECT PG_CREATE_LOGICAL_REPLICATION_SLOT('test_replication', 'pgoutput');
```
![image](https://github.com/user-attachments/assets/8fc122d5-bd72-47ed-80a3-bf56e602711c)

## Create the Datastream resources and start replication
1. From the search menu, type Datastream and select Datastream
![image](https://github.com/user-attachments/assets/d40af406-3322-4324-b56c-38fd8d52e84c)

2. Click Enable to enable the Datastream API
![image](https://github.com/user-attachments/assets/08be8691-5aa2-4a4e-9bb7-836ec0024dfd)

![image](https://github.com/user-attachments/assets/7f0d7dff-aa6d-43fd-890d-4049084c026e)


### **Create connection profiles**
1. In the Cloud console, navigate to the Connection Profiles tab and click Create Profile.
![image](https://github.com/user-attachments/assets/abdacbeb-2490-427b-8de5-941d564adcae)

2. Select the PostgreSQL connection profile type.
![image](https://github.com/user-attachments/assets/7a19d0fc-7e83-4238-8278-8cf29e960e16)

3. Use postgres-cp as the name and ID of the connection profile.
![image](https://github.com/user-attachments/assets/10e24b98-4f0e-4c76-a5ce-9c30de1b1585)

4. Enter the database connection details:
   - Region: europe-west4
   - The IP and port of the Cloud SQL instance created earlier
   - Username: postgres
   - Password: pwd
   - Database: postgres
5. Click Continue.
![image](https://github.com/user-attachments/assets/270e6053-a520-4ab5-8513-75798826e017)

![image](https://github.com/user-attachments/assets/946f8617-fd90-40e3-8ba6-2d073e546c8c)

6. Select the IP allowlisting connectivity method, and click Continue.
![image](https://github.com/user-attachments/assets/421d5e1d-5279-40f9-886e-a25a3bb44526)

7. Click RUN TEST to make sure that Datastream can reach the database.
![image](https://github.com/user-attachments/assets/073119c9-982e-4ff9-b3e1-a6e6188e5c07)

![image](https://github.com/user-attachments/assets/8189a231-ad9a-4611-81a2-225561eb83de)

8. Click Create.
![image](https://github.com/user-attachments/assets/f3e895aa-2da3-40e1-9509-6a4cb7f089d8)

![image](https://github.com/user-attachments/assets/66615169-5cc6-480e-aa95-fd7fe7b235c7)

### **BigQuery connection profile**
1. In the Cloud console, navigate to the Connection Profiles tab and click Create Profile.
![image](https://github.com/user-attachments/assets/2dc076a7-9ffd-4120-8013-3ff63862250c)

2. Select the BigQuery connection profile type.
![image](https://github.com/user-attachments/assets/d1a6d2c0-8fe0-47d3-939e-e95d0827d70e)

3. Use bigquery-cp as the name and ID of the connection profile.
4. Region europe-west4
5. Click Create.
![image](https://github.com/user-attachments/assets/1f21ddc1-aea7-4a23-a7fc-9a2c2084ead7)

![image](https://github.com/user-attachments/assets/b2f06b13-01d6-4a10-852c-9446ecb46bb6)

## Create stream
1. In the Cloud console, navigate to the Streams tab and click Create Stream.
![image](https://github.com/user-attachments/assets/842ba3dd-0150-4b90-b32e-10f8b7a6771f)

**Define the stream details**
1. Use test-stream as the name and ID of the stream.
2. Region europe-west4
3. Select PostgreSQL as the source type
4. Select BigQuery as destination type
5. Click **CONTINUE**.
![image](https://github.com/user-attachments/assets/1106a495-0ebf-47c6-ad0c-8a2c431a3997)

**Define the source**
1. Select the postgres-cp connection profile created in the previous step.
2. [Optional] Test connectivity by clicking RUN TEST
3. Click **CONTINUE**.
![image](https://github.com/user-attachments/assets/7a0626fe-e5b8-4f5f-a901-6ce7ab46b3e1)

Configure the source
Specify the replication slot name as test_replication.
Specify the publication name as test_publication.
![image](https://github.com/user-attachments/assets/42efb64f-a931-4f69-b88d-6d2cbae7af3d)

Select the test schema for replication.
Click Continue.
![image](https://github.com/user-attachments/assets/c64cfe42-4d4c-4c0c-b4c5-d5e354238264)

Define the destination
Select the bigquery-cp connection profile created in the previous step, then click Continue.
![image](https://github.com/user-attachments/assets/706e73c0-13f5-49fb-8f5d-3270beb69afe)

Configure the destination
Choose Region and select europe-west4 as the BigQuery dataset location.
Set the staleness limit to 0 seconds.
Click Continue.
![image](https://github.com/user-attachments/assets/9d10c4d3-11ff-49d3-a6a1-21589bddc7b9)

![image](https://github.com/user-attachments/assets/5613c6bc-aad4-4c20-8a0d-810395cfa3d7)

Review and create the stream
Finally, validate the stream details by clicking RUN VALIDATION. Once validation completes successfully, click CREATE AND START.
![image](https://github.com/user-attachments/assets/c5289d8d-3d9f-4f19-8f06-fd2434c4a119)

![image](https://github.com/user-attachments/assets/84bbe2bf-f6e2-4aad-aa01-2e6643a3778c)

![image](https://github.com/user-attachments/assets/231522c9-389c-498c-a05b-bd23163687d0)


## **View the data in BigQuery**
In the Google Cloud console, from the Navigation menu go to BigQuery.
In the BigQuery Studio explorer, expand the project node to see the list of datasets.
Expand the test dataset node.
Click on the example_table table.
Click on the PREVIEW tab to see the data in BigQuery.
```
Note: The data might take few minutes to appear in Preview section.
```
![image](https://github.com/user-attachments/assets/3962b5d6-5d6d-4236-99d9-d87d50d87ca2)

## **Check that changes in the source are replicated to BigQuery**
Run the following command in Cloud Shell to connect to the Cloud SQL database (the password is pwd):
```
gcloud sql connect postgres-db --user=postgres
```
Run the following SQL commands to make some changes to the data:
```
INSERT INTO test.example_table (text_col, int_col, date_col) VALUES
('abc', 0, '2022-10-01 00:00:00'),
('def', 1, NULL),
('ghi', -987, NOW());

UPDATE test.example_table SET int_col=int_col*2; 

DELETE FROM test.example_table WHERE text_col = 'abc';
```
![image](https://github.com/user-attachments/assets/af29fcf1-bb32-4461-9b8f-1b7a5711a9ec)

Open the BigQuery SQL workspace and run the following query to see the changes in BigQuery:
```
SELECT * FROM test.example_table ORDER BY id;
```
![image](https://github.com/user-attachments/assets/50a0fb9a-b310-4db4-861e-9976d10d3b2c)

