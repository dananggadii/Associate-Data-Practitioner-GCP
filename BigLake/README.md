# BigLake

![image](https://github.com/user-attachments/assets/59120c2f-9a4b-4485-b6f0-7cb58a23e7e4)

## Objectives
In this lab, you will:

- Create and view a connection resource.
- Set up access to a Cloud Storage data lake.
- Create a BigLake table.
- Query a BigLake table through BigQuery.
- Set up access control policies.
- Upgrade external tables to BigLake tables.

##

### Create a connection resource
1. From the Navigation Menu, go to BigQuery > BigQuery Studio. Click Done.

![image](https://github.com/user-attachments/assets/9b2af59a-ff3e-46bc-a18a-51dd111bd435)

2. To create a connection, click +ADD, and then click Connections to external data sources.
```
Note: If you are prompted to enable the BigQuery Connection API click Enable API.
```

![image](https://github.com/user-attachments/assets/c13f4be2-2d90-4471-810e-50953716fcd8)

![image](https://github.com/user-attachments/assets/fb6f1815-524b-4d6f-92ef-76e660090219)

3. In the Connection type list, select Vertex AI remote models, remote functions and BigLake (Cloud Resource).

![image](https://github.com/user-attachments/assets/c10eaa1e-6430-4ec4-a414-e308a62b8f2f)

4. In the Connection ID field, enter my-connection.
5. For Location type, choose **Multi-region** and select **US (multiple regions in United States)** from dropdown.
6. Click **Create connection**.

![image](https://github.com/user-attachments/assets/a595fcf5-8cb7-4bab-9d86-130b83d88423)

7. To view your connection information, select the connection in the navigation menu.
8. In the **Connection info** section, copy the Service Account ID. You will need this in the following section.

![image](https://github.com/user-attachments/assets/1a356610-9cee-4125-92c7-8bb8961f1014)

### Set up access to a Cloud Storage data lake
1. From the Navigation Menu, go to IAM & Admin > IAM.

2. Click +GRANT ACCESS.

3. In the New principals field, enter the service account ID that you copied earlier.

4. In the Select a role field, select Cloud Storage, and then select Storage Object Viewer.

5. Click Save.
```
Note: After you migrate users to BigLake tables, remove direct Cloud Storage permissions from existing users. Direct file access allows users to bypass governance policies (such as row- and column-level security) set on BigLake tables.
```

### Create a BigLake table
#### Create a dataset
1. Navigate back to BigQuery > BigQuery Studio.

2. Click the three dots next to your project name and select Create dataset.

3. For the Dataset ID, use demo_dataset.

4. For Location type, choose Multi-region and select US (multiple regions in United States) from dropdown.

5. Leave the rest of the fields as default and click Create Dataset.

6. Now that you have a dataset created, you can copy an existing dataset from Cloud Storage into BigQuery.

#### Create the table
1. Click three dots next to demo_dataset, then choose Create table.

2. Under Source for Create table from, choose Google Cloud Storage.
```
Note: A Cloud Storage bucket has been created with two datasets that you will use in this lab.
```

3. Click Browse to select the dataset. Navigate to the bucket named as Project ID and then customer.csv file to import it into BigQuery, and click Select.

4. Under Destination, verify your lab project has been selected and you're using the demo_dataset.

5. For the table name, use biglake_table.

6. Set the table type to External Table.

7. Select the box to Create a BigLake table using a Cloud Resource connection.
Verify that your connection ID us.my-connection is selected. Your configuration should resemble the following:

8. Under Schema, enable Edit as text and copy and paste the following schema into the text box:
```
[
{
    "name": "customer_id",
    "type": "INTEGER",
    "mode": "REQUIRED"
  },
  {
    "name": "first_name",
    "type": "STRING",
    "mode": "REQUIRED"
  },
  {
    "name": "last_name",
    "type": "STRING",
    "mode": "REQUIRED"
  },
  {
    "name": "company",
    "type": "STRING",
    "mode": "NULLABLE"
  },
  {
    "name": "address",
    "type": "STRING",
    "mode": "NULLABLE"
  },
  {
    "name": "city",
    "type": "STRING",
    "mode": "NULLABLE"
  },
  {
    "name": "state",
    "type": "STRING",
    "mode": "NULLABLE"
  },
  {
    "name": "country",
    "type": "STRING",
    "mode": "NULLABLE"
  },
  {
    "name": "postal_code",
    "type": "STRING",
    "mode": "NULLABLE"
  },
  {
    "name": "phone",
    "type": "STRING",
    "mode": "NULLABLE"
  },
  {
    "name": "fax",
    "type": "STRING",
    "mode": "NULLABLE"
  },
  {
    "name": "email",
    "type": "STRING",
    "mode": "REQUIRED"
  },
  {
    "name": "support_rep_id",
    "type": "INTEGER",
    "mode": "NULLABLE"
  }
]
```

9. Click Create Table.

### Query a BigLake table through BigQuery
1. From the biglake_table preview toolbar, click Query > In new tab.

2. Run the following to query the BigLake table through the BigQuery Editor:
```
SELECT * FROM `Project ID.demo_dataset.biglake_table`
```

3. Click Run.

4. Verify you can see all of the columns and data in the resulting table.

### Set up access control policies
#### Add policy tags to columns
1. From the Navigation Menu, go to BigQuery > BigQuery Studio.

2. Navigate to demo-dataset > biglake_table and click the table to open the table schema page.

3. Click Edit Schema.

4. Check the boxes next to the address, postal_code, and phone fields.

5. Click Add policy tag.

6. Click taxonomy name to expand it to select biglake-policy.

7. Click Select.
Your columns should now have the policy tags attached to them.

8. Click Save.

9. Verify your table schema now resembles the following.

#### Verify the column level security
1. Open the query editor for the biglake_table.

2. Run the following to query the BigLake table through the BigQuery Editor:
```
SELECT * FROM `Project ID.demo_dataset.biglake_table`
```

3. Click Run.
You should receive an error access denied error:

4. Now, run the following query, omitting the columns you don't have access to:
```
SELECT *  EXCEPT(address, phone, postal_code)
FROM `Project ID.demo_dataset.biglake_table`
```

### Upgrade external tables to BigLake tables
#### Create the external table
1. Click three dots next to demo_dataset, then choose Create table.

2. Under Source for Create table from, choose Google Cloud Storage.

3. Click Browse to select the dataset. Navigate to the bucket named Project ID and then invoice.csv file to import it into BigQuery, and click Select.

4. Under Destination, verify your lab project has been selected and you're using the demo_dataset.

5. For the table name, use external_table.

6. Set the table type to External Table.

7. Under Schema, enable Edit as text and copy and paste the following schema into the text box:
```
[
{
    "name": "invoice_id",
    "type": "INTEGER",
    "mode": "REQUIRED"
  },
  {
    "name": "customer_id",
    "type": "INTEGER",
    "mode": "REQUIRED"
  },
  {
    "name": "invoice_date",
    "type": "TIMESTAMP",
    "mode": "REQUIRED"
  },
  {
    "name": "billing_address",
    "type": "STRING",
    "mode": "NULLABLE"
  },
  {
    "name": "billing_city",
    "type": "STRING",
    "mode": "NULLABLE"
  },
  {
    "name": "billing_state",
    "type": "STRING",
    "mode": "NULLABLE"
  },
  {
    "name": "billing_country",
    "type": "STRING",
    "mode": "NULLABLE"
  },
  {
    "name": "billing_postal_code",
    "type": "STRING",
    "mode": "NULLABLE"
  },
  {
    "name": "total",
    "type": "NUMERIC",
    "mode": "REQUIRED"
  }
]
```

8. Click Create Table.

#### Update external table to Biglake table
1. Open a new Cloud Shell window and run the following command to generate a new external table definition that specifies the connection to use:
```
export PROJECT_ID=$(gcloud config get-value project)
bq mkdef \
--autodetect \
--connection_id=$PROJECT_ID.US.my-connection \
--source_format=CSV \
"gs://$PROJECT_ID/invoice.csv" > /tmp/tabledef.json
```

2. Verify your table definition has been created:
```
cat /tmp/tabledef.json
```

3. Get the schema from your table:
```
bq show --schema --format=prettyjson  demo_dataset.external_table > /tmp/schema
```

4 Update the table using the new external table definition:
```
bq update --external_table_definition=/tmp/tabledef.json --schema=/tmp/schema demo_dataset.external_table
```

#### Verify the updated table
1. From the Navigation Menu, go to BigQuery > BigQuery Studio.

2. Navigate to demo-dataset > and double click external_table.

3. Open the Details tab.

4. Verify under External Data Configuration that the table is now using the proper Connection ID.

