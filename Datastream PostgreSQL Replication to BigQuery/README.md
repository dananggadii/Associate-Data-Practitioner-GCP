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
