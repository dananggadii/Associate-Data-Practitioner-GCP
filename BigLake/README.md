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

### Create a connection resource
1. From the Navigation Menu, go to BigQuery > BigQuery Studio. Click Done.

2. To create a connection, click +ADD, and then click Connections to external data sources.
```
Note: If you are prompted to enable the BigQuery Connection API click Enable API.
```

3. In the Connection type list, select Vertex AI remote models, remote functions and BigLake (Cloud Resource).

4. In the Connection ID field, enter my-connection.

5. For Location type, choose **Multi-region** and select **US (multiple regions in United States)** from dropdown.

6. Click **Create connection**.

7. To view your connection information, select the connection in the navigation menu.

8. In the **Connection info** section, copy the Service Account ID. You will need this in the following section.

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
