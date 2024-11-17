# Create and Execute a SQL Workflow in Dataform

## Learning objectives
1. Create a Dataform repository.
2. Create and initialize a Dataform development workspace.
3. Create and execute a SQL workflow.
4. View execution logs in Dataform.

##

### Create a Dataform repository
1. In the Console, expand the Navigation menu, then select BigQuery > Dataform.
2. Click CREATE REPOSITORY.


![image](https://github.com/user-attachments/assets/95b85d7f-dd84-4462-ad41-3e3b47382a46)

3. On the Create repository page, do the following:
- In the Repository ID field, enter quickstart-repository.
- In the Region list, select REGION.
- Click CREATE.
```
Once the repository is created, you will see the Dataform service account. Please copy this down, so you can use it later to assign necessary permissions.
```


![image](https://github.com/user-attachments/assets/3ddc9619-7ef4-4ed9-9d8b-6d9cf7cb6d5d)

- Click Go to Repositories.
```
Note: If you get permission denied error related to API request wait for few minutes and create the repository again.
```


![image](https://github.com/user-attachments/assets/3ee08ba8-baa6-424a-9bcb-a7802b191743)


![image](https://github.com/user-attachments/assets/a547e473-e9d5-4326-b44b-4ab7bab7ece0)

### Create and initialize a Dataform development workspace
1. On the Dataform page, click on the quickstart-repository repository you just created.
2. Click CREATE DEVELOPMENT WORKSPACE.


![image](https://github.com/user-attachments/assets/7fe9c8cd-3957-40d6-b36c-06258e620459)

3. In the Create development workspace window, do the following:
- In the Workspace ID field, enter quickstart-workspace.
- Click CREATE.


![image](https://github.com/user-attachments/assets/a6528b82-0e7e-4bc8-b5cc-704df8e9f778)

4. Once created, click on the quickstart-workspace development workspace.
5. Click INITIALIZE WORKSPACE.


![image](https://github.com/user-attachments/assets/f7fd89d4-fedf-459e-bf6d-dead910a5150)

### Create a SQLX file for defining a view
In this section, you define a view that you will later use as a data source for a table.
1. In the Files pane, next to definitions, click the More menu.
2. Click Create file.


![image](https://github.com/user-attachments/assets/3b5b9d9f-fccd-4d37-83e6-8b5b09ec85e0)

3. In the Create new file pane, do the following:
- In the Add a file path field, enter definitions/quickstart-source.sqlx.
- Click CREATE FILE.


![image](https://github.com/user-attachments/assets/85da2564-7e15-4911-967c-d19e13e56cc7)

#### Define a view
1. In the Files pane, expand the definitions folder.
2. Click quickstart-source.sqlx.
3. In the file, enter the following code snippet:
```
config {
  type: "view"
}

SELECT
  "apples" AS fruit,
  2 AS count
UNION ALL
SELECT
  "oranges" AS fruit,
  5 AS count
UNION ALL
SELECT
  "pears" AS fruit,
  1 AS count
UNION ALL
SELECT
  "bananas" AS fruit,
  0 AS count
```

![image](https://github.com/user-attachments/assets/ffa65756-5573-4858-98b3-adfcd13cb1de)

### Create a SQLX file for table definition
In the following sections, you define the table type in a SQLX file, and then write a SELECT statement to define the table structure within the same file.
1. In the Files pane, next to definitions, click the More menu, and then select Create file.


![image](https://github.com/user-attachments/assets/76ed7d24-36d5-4c2b-9aca-07602067022b)

2. In the Add a file path field, enter definitions/quickstart-table.sqlx.
3. Click CREATE FILE.


![image](https://github.com/user-attachments/assets/1fd4083b-2d9a-4585-9720-7dd214d62712)

#### Define the table type, structure and dependencies
1. In the Files pane, expand the definitions directory.
2. Select quickstart-table.sqlx, and then enter the following table type and SELECT statement:
```
config {
  type: "table"
}

SELECT
  fruit,
  SUM(count) as count
FROM ${ref("quickstart-source")}
GROUP BY 1
```
```
Note: You might notice an error note in the compiled queries section. Ignore the message and proceed to further steps to execute the workflow.
```


![image](https://github.com/user-attachments/assets/4da6ea6d-2e1f-4d32-8e86-924b872ad046)

### Grant Dataform access to BigQuery
1. In the Google Cloud console, on the Navigation menu (Navigation menu icon), select IAM & Admin > IAM.
2. Click VIEW BY PRINCIPALS. Next, click GRANT ACCESS
3. In the New principals field, enter your Dataform service account ID.
4. In the Select a role drop-down list, select the BigQuery Job User role.
5. Click Add another role, and then in the Select a role drop-down list, select the BigQuery Data Editor role.
6. Click Add another role, and then in the Select a role drop-down list, select the BigQuery Data Viewer role.
7. Click Save.

![image](https://github.com/user-attachments/assets/6cdd31d9-9505-4a8c-8ff6-8274bdd196e5)

![image](https://github.com/user-attachments/assets/42512b37-11f1-4b46-975a-f3f17370cf1e)

### Execute the workflow
1. In the Console, go to Navigation Menu > BigQuery > Dataform.
2. Click on quickstart-repository to open the repository.
3. Click on quickstart-workspace to open the development workspace.
4. On the quickstart-workspace page, click START EXECUTION.
5. Click Execute actions.

![image](https://github.com/user-attachments/assets/1f469904-037b-4090-ae2c-ad960d76a98c)

6. Click All actions tab.
7. In the Execute pane, click START EXECUTION.
```
Dataform uses the default repository settings to create the contents of your workflow in a BigQuery dataset called dataform.
```

![image](https://github.com/user-attachments/assets/600e627c-946e-43ec-9ed9-f1e673f157ca)

#### View execution logs
1. On the quickstart-workspace page, click EXECUTIONS to open the Executions pane.
2. To view details of your execution, click the latest execution.

![image](https://github.com/user-attachments/assets/3127e865-42d0-4af2-973f-6e45f5d20a8c)

![image](https://github.com/user-attachments/assets/8e7d7e7e-3c5f-4020-ba93-80f6b99f3b43)
