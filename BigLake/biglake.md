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

![image](https://github.com/user-attachments/assets/f0a9bc12-0040-4546-aa2c-4550db48a89f)

3. In the New principals field, enter the service account ID that you copied earlier.

![image](https://github.com/user-attachments/assets/28766eca-a373-42d9-87a2-bff8cfb1220f)

![image](https://github.com/user-attachments/assets/67e51e0c-b24b-42b8-bbf6-753b2b1b616a)

4. In the Select a role field, select Cloud Storage, and then select Storage Object Viewer.
5. Click Save.
```
Note: After you migrate users to BigLake tables, remove direct Cloud Storage permissions from existing users. Direct file access allows users to bypass governance policies (such as row- and column-level security) set on BigLake tables.
```

![image](https://github.com/user-attachments/assets/238ed2f1-6c8b-4a6e-b7e9-816bf28ab158)

![image](https://github.com/user-attachments/assets/4127bc76-ed63-447c-a8bb-2b34bbf6fc68)

### Create a BigLake table
#### Create a dataset
1. Navigate back to BigQuery > BigQuery Studio.
2. Click the three dots next to your project name and select Create dataset.

![image](https://github.com/user-attachments/assets/eeb2d7ec-b41f-4d12-bae2-29baeb133791)

3. For the Dataset ID, use demo_dataset.
4. For Location type, choose Multi-region and select US (multiple regions in United States) from dropdown.
5. Leave the rest of the fields as default and click Create Dataset.
6. Now that you have a dataset created, you can copy an existing dataset from Cloud Storage into BigQuery.

![image](https://github.com/user-attachments/assets/1752b169-a8a8-4629-bbfe-109b335599d0)

#### Create the table
1. Click three dots next to demo_dataset, then choose Create table.

![image](https://github.com/user-attachments/assets/5b581de4-10a1-4fb4-ac16-036b89673558)

2. Under Source for Create table from, choose Google Cloud Storage.
```
Note: A Cloud Storage bucket has been created with two datasets that you will use in this lab.
```
3. Click Browse to select the dataset. Navigate to the bucket named as Project ID and then customer.csv file to import it into BigQuery, and click Select.

![image](https://github.com/user-attachments/assets/40a310e5-d0da-4eb6-8d6c-4a985453f88e)

![image](https://github.com/user-attachments/assets/7bcfdaaf-bf23-4870-8f42-30c69ca42b3a)

4. Under Destination, verify your lab project has been selected and you're using the demo_dataset.
5. For the table name, use biglake_table.
6. Set the table type to External Table.
7. Select the box to Create a BigLake table using a Cloud Resource connection.
Verify that your connection ID us.my-connection is selected. Your configuration should resemble the following:

![image](https://github.com/user-attachments/assets/041ddfec-6806-4ce8-a5f7-f9f78a6a2f23)

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

![image](https://github.com/user-attachments/assets/e78048ec-ccfb-4693-be93-39485c3f513a)

### Query a BigLake table through BigQuery
1. From the biglake_table preview toolbar, click Query > In new tab.

![image](https://github.com/user-attachments/assets/a83a3d71-f77e-44c5-a377-05f2bdea9e03)

2. Run the following to query the BigLake table through the BigQuery Editor:
```
SELECT * FROM `Project ID.demo_dataset.biglake_table`
```
3. Click Run.
4. Verify you can see all of the columns and data in the resulting table.

![image](https://github.com/user-attachments/assets/ba00b648-0e74-43af-bd7c-945c21cfadc6)

### Set up access control policies
#### Add policy tags to columns
1. From the Navigation Menu, go to BigQuery > BigQuery Studio.
2. Navigate to demo-dataset > biglake_table and click the table to open the table schema page.
3. Click Edit Schema.

![image](https://github.com/user-attachments/assets/705d9a6b-aee9-4d3b-b961-44f0ae004826)

4. Check the boxes next to the address, postal_code, and phone fields.
5. Click Add policy tag.
6. Click taxonomy name to expand it to select biglake-policy.
7. Click Select.
```
Your columns should now have the policy tags attached to them.
```
8. Click Save.

![image](https://github.com/user-attachments/assets/97fef81d-7166-4c34-9173-f7bc0844b8ed)

9. Verify your table schema now resembles the following.

![image](https://github.com/user-attachments/assets/db7e7ac2-2884-46f3-882a-8f88539bda12)

#### Verify the column level security
1. Open the query editor for the biglake_table.
2. Run the following to query the BigLake table through the BigQuery Editor:
```
SELECT * FROM `Project ID.demo_dataset.biglake_table`
```
3. Click Run.
You should receive an error access denied error:

![image](https://github.com/user-attachments/assets/e9b8f3bd-0cf4-40a0-a0db-b45e55330676)

4. Now, run the following query, omitting the columns you don't have access to:
```
SELECT *  EXCEPT(address, phone, postal_code)
FROM `Project ID.demo_dataset.biglake_table`
```

![image](https://github.com/user-attachments/assets/5179dd29-0338-4e8b-8b7e-2af44a84481e)

### Upgrade external tables to BigLake tables
#### Create the external table
1. Click three dots next to demo_dataset, then choose Create table.

![image](https://github.com/user-attachments/assets/0d12df75-5215-4efd-b0ed-f9f3aeafea85)

2. Under Source for Create table from, choose Google Cloud Storage.
3. Click Browse to select the dataset. Navigate to the bucket named Project ID and then invoice.csv file to import it into BigQuery, and click Select.

![image](https://github.com/user-attachments/assets/3763ad14-8517-407d-a277-d80088944781)

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

![image](https://github.com/user-attachments/assets/4c46b131-4636-4e12-8979-bec120ab9e20)

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

![image](https://github.com/user-attachments/assets/b5f7f423-5859-482f-af48-c09e166c2454)

#### Verify the updated table
1. From the Navigation Menu, go to BigQuery > BigQuery Studio.
2. Navigate to demo-dataset > and double click external_table.
3. Open the Details tab.
4. Verify under External Data Configuration that the table is now using the proper Connection ID.

![image](https://github.com/user-attachments/assets/b831c7e5-dbe3-40a1-9ca4-e9d8d6e179e4)

