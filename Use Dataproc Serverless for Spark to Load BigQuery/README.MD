# Use Dataproc Serverless for Spark to Load BigQuery

## What you'll do
1. Configure the environment
2. Download lab assets
3. Configure and execute the Spark code
4. View data in BigQuery

### Complete environment configuration tasks
First, you're going to perform a few enivronment configuration tasks to support the execution of a Dataproc Serverless workload.
1. In the Cloud Shell, run the following command to enable Private IP Access:
```
gcloud compute networks subnets update default --region=REGION --enable-private-ip-google-access
```
2. Use the following command to create a new Cloud Storage bucket as a staging location:
```
gsutil mb -p  PROJECT_ID gs://PROJECT_ID
```
3. Use the following command to create a new Cloud Storage bucket as temporary location for BigQuery while it creates and loads a table:
```
gsutil mb -p  PROJECT_ID gs://PROJECT_ID-bqtemp
```
4. Create a BQ dataset to store the data.
```
bq mk -d  loadavro
```

