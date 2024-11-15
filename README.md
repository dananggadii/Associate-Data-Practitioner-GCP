# Loading data into BigQuery

### 1. Open the sidebar panel.
![image](https://github.com/user-attachments/assets/e18c25ef-4269-4504-9c21-11caec78a7c8)

### 2. Click BigQuery.
![image](https://github.com/user-attachments/assets/847c6107-aa90-4e1a-85d0-a2e20b4458b7)

### 3. If a message box appears, click Done.
![image](https://github.com/user-attachments/assets/4caa4251-f1bb-49b6-95a4-2a130144fc32)

### 4. To create a new dataset, click the View Action Icon (three-dot icon) on the project ID and select Create Dataset.
![image](https://github.com/user-attachments/assets/1325fddb-027a-42d2-ae7d-91ed1de4f4e2)

### 5. Fill in the dataset name > Location type > [optional] External dataset (if the dataset is on Cloud Spanner) > click Create Dataset.
![image](https://github.com/user-attachments/assets/b151f4ef-37c1-4025-8aba-c4f39c765776)

![image](https://github.com/user-attachments/assets/a2c202c5-3e0f-49fe-8e95-27591f8acfa7)

### 6. Create a table from the dataset we just created > click the View Action Icon on the dataset > Create Table.
![image](https://github.com/user-attachments/assets/3e8ebc40-77f3-4910-8658-1b735615e8aa)

### 7. Under Source, choose Create Table From and select Upload > browse for the dataset from your local PC > enter the table name > check Auto-detect Schema > click Create Table.
![image](https://github.com/user-attachments/assets/65a04641-bff3-479d-9ce5-07bb43b65da8)

![image](https://github.com/user-attachments/assets/610fe100-b009-400d-a8e8-b3c65b838c40)

![image](https://github.com/user-attachments/assets/d92f593f-b168-496a-80e3-3664284fa55d)

![image](https://github.com/user-attachments/assets/e6dbf788-1b14-4601-8266-d0e78fa93a44)

### 8. Click the table we created > select the Details tab to view the dataset details > select the Preview tab to view the table dataset.
![image](https://github.com/user-attachments/assets/367d29bc-ecc5-46c7-97cb-48b4678497d9)

![image](https://github.com/user-attachments/assets/24fa01e7-31ca-4445-8db0-2aaaef674f39)

### 9. To query the dataset, click Query > Open in New Tab > write the command below to view the data > click Run.
```
#standardSQL
SELECT
  *
FROM
  nyctaxi.2018trips
ORDER BY
  fare_amount DESC
LIMIT  5
```
![image](https://github.com/user-attachments/assets/73ba3a1c-6148-4858-a5fc-de6a409d7e07)

![image](https://github.com/user-attachments/assets/34f50388-1326-492c-af21-09caa21003af)

![image](https://github.com/user-attachments/assets/562d4291-9592-47dd-82bc-aab106c15d18)

### 10. To create a dataset from Cloud Storage using Cloud Shell, click the Cloud Shell Icon.
![image](https://github.com/user-attachments/assets/df707bd2-38c6-4218-8965-e37a4321f1d3)

### 11. Write the command below to load the dataset from Cloud Storage.
```
bq load \
--source_format=CSV \
--autodetect \
--noreplace  \
nyctaxi.2018trips \
gs://cloud-training/OCBL013/nyc_tlc_yellow_trips_2018_subset_2.csv

```
![image](https://github.com/user-attachments/assets/c0af6c65-8929-475d-b864-c6ba7de7639c)

### 12. Next, type the command below to create a table.
```
#standardSQL
CREATE TABLE
  nyctaxi.january_trips AS
SELECT
  *
FROM
  nyctaxi.2018trips
WHERE
  EXTRACT(Month
  FROM
    pickup_datetime)=1;

```
![image](https://github.com/user-attachments/assets/4946a02b-b9f0-4999-9320-4902b09638c2)

### 13. Check the data in the table using the query below.
```
#standardSQL
SELECT
  *
FROM
  nyctaxi.january_trips
ORDER BY
  trip_distance DESC
LIMIT
  1

```
![image](https://github.com/user-attachments/assets/b0185569-3dc8-4568-bf64-93c818f30dff)

