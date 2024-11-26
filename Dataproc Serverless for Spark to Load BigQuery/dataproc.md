# Use Dataproc Serverless for Spark to Load BigQuery

### Configuration tasks to support the execution of a Dataproc Serverless workload.

1. In the Cloud Shell, run the following command to enable Private IP Access:

```bash
gcloud compute networks subnets update default --region=REGION --enable-private-ip-google-access
```

2. Use the following command to create a new Cloud Storage bucket as a staging location:

```bash
gsutil mb -p  PROJECT_ID gs://PROJECT_ID
```

3. Use the following command to create a new Cloud Storage bucket as temporary location for BigQuery while it creates and loads a table:

```bash
gsutil mb -p  PROJECT_ID gs://PROJECT_ID-bqtemp
```

4. Create a BQ dataset to store the data.

```bash
bq mk -d  loadavro
```

### Download lab assets

1. From the Navigation menu click on Compute Engine. Here you'll see a linux VM provisioned for you. Click the SSH button next to the lab-vm instance.

2. At the VM terminal prompt, download the Avro file that will be processed for storage in BigQuery.

```bash
wget https://storage.googleapis.com/cloud-training/dataengineering/lab_assets/idegc/campaigns.avro
```

3. Next, move the Avro file to the staging Cloud Storage bucket you created earlier.

```bash
gcloud storage cp campaigns.avro gs://PROJECT_ID
```

4. Download an archive containing the Spark code to be executed against the Serverless environment.

```bash
wget https://storage.googleapis.com/cloud-training/dataengineering/lab_assets/idegc/dataproc-templates.zip
```

5. Extract the archive.

```bash
unzip dataproc-templates.zip
```

6. Change to the Python directory.

```bash
cd dataproc-templates/python
```

### Configure and execute the Spark code

1. Set the following environment variables for the Dataproc Serverless environment.

```bash
export GCP_PROJECT=PROJECT_ID
export REGION=REGION
export GCS_STAGING_LOCATION=gs://PROJECT_ID
export JARS=gs://cloud-training/dataengineering/lab_assets/idegc/spark-bigquery_2.12-20221021-2134.jar
```

2. Run the following code to execute the Spark Cloud Storage to BigQuery template to load the Avro file in to BigQuery.

```bash
./bin/start.sh \
-- --template=GCSTOBIGQUERY \
    --gcs.bigquery.input.format="avro" \
    --gcs.bigquery.input.location="gs://PROJECT_ID" \
    --gcs.bigquery.input.inferschema="true" \
    --gcs.bigquery.output.dataset="loadavro" \
    --gcs.bigquery.output.table="campaigns" \
    --gcs.bigquery.output.mode=overwrite\
    --gcs.bigquery.temp.bucket.name="PROJECT_ID-bqtemp"
```

> **Note**: You may safely ignore any warning stating: **WARN FileStreamSink: Assume no metadata directory. Error while looking for metadata directory in the path...** Because this is a small test, a metadata directory is not required.

### Confirm that the data was loaded into BigQuery

1. View the data in the new table in BigQuery.

```bash
bq query \
 --use_legacy_sql=false \
 'SELECT * FROM `loadavro.campaigns`;'
```

2. The query should return results similiar to the following:
   Example output:
