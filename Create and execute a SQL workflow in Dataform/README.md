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


3. On the Create repository page, do the following:
- In the Repository ID field, enter quickstart-repository.
- In the Region list, select REGION.
- Click CREATE.
```
Once the repository is created, you will see the Dataform service account. Please copy this down, so you can use it later to assign necessary permissions.
```


- Click Go to Repositories.
```
Note: If you get permission denied error related to API request wait for few minutes and create the repository again.
```


### Create and initialize a Dataform development workspace
1. On the Dataform page, click on the quickstart-repository repository you just created.
2. Click CREATE DEVELOPMENT WORKSPACE.


3. In the Create development workspace window, do the following:
- In the Workspace ID field, enter quickstart-workspace.
- Click CREATE.


4. Once created, click on the quickstart-workspace development workspace.
5. Click INITIALIZE WORKSPACE.


### Create a SQLX file for defining a view
In this section, you define a view that you will later use as a data source for a table.
1. In the Files pane, next to definitions, click the More menu.
2. Click Create file.


3. In the Create new file pane, do the following:
- In the Add a file path field, enter definitions/quickstart-source.sqlx.
- Click CREATE FILE.


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


### Create a SQLX file for table definition
In the following sections, you define the table type in a SQLX file, and then write a SELECT statement to define the table structure within the same file.
1. In the Files pane, next to definitions, click the More menu, and then select Create file.


2. In the Add a file path field, enter definitions/quickstart-table.sqlx.
3. Click CREATE FILE.


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


### Grant Dataform access to BigQuery
1. In the Google Cloud console, on the Navigation menu (Navigation menu icon), select IAM & Admin > IAM.
2. Click VIEW BY PRINCIPALS. Next, click GRANT ACCESS
3. In the New principals field, enter your Dataform service account ID.
4. In the Select a role drop-down list, select the BigQuery Job User role.
5. Click Add another role, and then in the Select a role drop-down list, select the BigQuery Data Editor role.
6. Click Add another role, and then in the Select a role drop-down list, select the BigQuery Data Viewer role.
7. Click Save.


### Execute the workflow
1. In the Console, go to Navigation Menu > BigQuery > Dataform.
2. Click on quickstart-repository to open the repository.
3. Click on quickstart-workspace to open the development workspace.
4. On the quickstart-workspace page, click START EXECUTION.


5. Click Execute actions.


6. Click All actions tab.


7. In the Execute pane, click START EXECUTION.
```
Dataform uses the default repository settings to create the contents of your workflow in a BigQuery dataset called dataform.
```


#### View execution logs
1. On the quickstart-workspace page, click EXECUTIONS to open the Executions pane.
2. To view details of your execution, click the latest execution.
