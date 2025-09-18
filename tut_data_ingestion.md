---

copyright:
  years: 2022, 2025
lastupdated: "2025-09-17"

keywords: ingestion, time travel, rollback,

subcollection: watsonxdata

content-type: tutorial
account-plan: paid
completion-time: 0.25h
---

{{site.data.keyword.attribute-definition-list}}
{:video: .video}

{:shortdesc: .shortdesc}
{:step: data-tutorial-type="step"}



# Data ingestion, Time travel, and Table rollback
{: #ingtutorial}
{: toc-content-type="tutorial"}
{: toc-completion-time="0.25h"}

This tutorial guides you through the process of ingesting data in {{site.data.keyword.lakehouse_short}}, performing time travel, and table roll back operations.
{: shortdesc}


Data ingestion
: Data ingestion is the process of importing and loading data into {{site.data.keyword.lakehouse_short}}. You can perform data ingestion in {{site.data.keyword.lakehouse_short}} in the following methods:

   * Ingesting data by using **Create table from file** option in the **Data manager** page.
   * Ingesting data by using SQL queries.
   * Ingesting data by using `IBM-lh` command-line tool.
   * Ingesting data by using Spark engine.

   For more information, see [Data ingestion](/docs/watsonxdata?topic=watsonxdata-load_ingest_data).

Time travel
: The Time travel capability in Apache Iceberg tables allows you to fetch and inspect the table history. It uses table snapshots to support the time travel functions. A table snapshot represents the state of a table at a particular point in time. Iceberg generates the table snapshot record when the table is created or modified (insert, update, delete). You can use this snapshot record to query to see the table details then.

Hive tables do not support the time travel feature.
{: note}


Rollback
: The table rollback feature allows you to roll back a table to a previous point in time by using table snapshots.

## Use Case Scenario
{: #ingtn_scrio}

Consider you are a Data Engineer for your company and you are tasked with managing Car records in the company database. Upload the existing data records in the storage. Add a new set of data to the existing table. After review, you see that the new set of data added is not appropriate and decide to rollback the table to a previous state.

The following video provides a visual method to learn the concepts and tasks in this documentation.

![Data ingestion, time travel, and table rollback in IBM watsonx.data](https://www.kaltura.com/p/1773841/sp/177384100/embedIframeJs/uiconf_id/27941801/partner_id/1773841?iframeembed=true&entry_id=1_qen8mlbx){: video output="iframe" data-script="none" id="mediacenterplayer" frameborder="0" width="560" height="315" allowfullscreen webkitallowfullscreen mozAllowFullScreen}




### Objective
{: #ingtn_obj}


* Create a table and load the sample data by using Spark engine to a table.
* Load more records into the `cars` table.
* Retrieve table records by using table snapshots.
* Perform table rollback operations.


### Before you begin
{: #bbingetn}

* Download the `cars.csv` file from (https://ibm.box.com/v/data-cars-csv).
* You must have a Lite plan instance provisioned.
* The Lite plan instance must include Spark and Presto engines in running state.
* Associate a catalog to both Presto and Spark engines. Here, Apache Iceberg catalog.


## Procedure
{: #ingestion}

## Creating table and loading data
{: #ingst_stp1}
{: step}

The section guides you through the procedure to create a table that is named `cars` and ingest data present `cars.csv` file by using Spark engine.

1. Log in to {{site.data.keyword.lakehouse_short}} console.

2. From the navigation menu, select **Data manager**.

3. Click **Ingest Data** and select **Local System**. For more information on how to ingest data, see [Ingesting data from local system](/docs/watsonxdata?topic=watsonxdata-ingest_spark_ui#spk_ingest_datalocal).

11. Click **Browse data** tab. Refresh the Iceberg catalog to view the new schema and table with data. You can view the Table columns, Time travel, Data sample, and DDL tabs.

12. Click **Time Travel**. You can view that the table has `406` records.


## Loading more records to the table
{: #ingst_stp2}
{: step}

Perform multiple transactions (two transactions) to update the `cars` table. In the first transaction, ingest two other car records for the model `TESLA` and in the second transaction, ingest one record for the model`Kia Optima`.

To do that:

1. Go to **Query workspace**.

2. Select **Presto** engine.


3. Use the following SQL query to insert the first set of data into the `cars` table.

   ```bash
   INSERT INTO iceberg_data.automobiles.cars VALUES
   ('Tesla Model S', 102, 0, 0, 670, 4766, 3.1, 2023, 'USA'),
   ('Tesla Model 3', 134, 0, 0, 283, 3582, 5.8, 2023, 'USA');
   ```
   {: codeblock}


4. Run the query. The data is added and the total record is `408`.

5. Use the following SQL query to insert the second set of data into the `cars` table.

   ```bash
   INSERT INTO iceberg_data.automobiles.cars VALUES
   ('Kia Optima', 27, 4, 2457, 185, 3200, 8.5, 2023, 'South Korea');
   ```
   {: codeblock}

4. Run the query. The data is added and the total record becomes `409`.

1. Go to **Data manager**.

2. Select the table `cars`. From the **cars** section, select the **Time travel** tab. You can view the snapshot records (with SnapshotID) corresponding to the data transactions.


## Retrieving table records by using table snapshots.
{: #ingst_stp3}
{: step}

This section of the tutorial guides you through the procedure to retrieve table records by using table snapshots. You run queries to retrieve data for auditing and regulatory purposes.

1. Go to **Query workspace**.

2. Run the following query to retrieve the snapshot records corresponding to the three insert transactions performed.

   ```bash
   SELECT * FROM iceberg_data.automobiles."cars$snapshots" ORDER BY committed_at;
   ```
   {: codeblock}

   The result set include three snapshot records with snapshot_id, date, time, and time zone.
   In this tutorial, the SnapshotID, date, time for each transaction are referred as: `<Tran1Time>`, `<Tran1SnapshotID>`, `<Tran2Time>`, `<Tran2SnapshotID>`, `<Tran3Time>`, and `<Tran3SnapshotID>`.

   You can also view the snapshot records from **Data manager** > `cars` table > **Time travel** tab.
   {: note}

3. Provide the snapshot ID or time in the following queries and run the queries to retrieve the table information at that point.


 | Scenario           | Query        |      Result       |
 |------------------|--------------------|----------|
 |Retrieve data from the initial state by using snapshot ID.    | `SELECT * FROM iceberg_data.automobiles.cars FOR VERSION AS OF <Tran1SnapshotID> ORDER BY Snapshot ID;` | Result section displays 406 records. |
 | Retrieve data from the initial state by using timestamp.| `SELECT * FROM iceberg_data.automobiles.cars FOR TIMESTAMP AS OF CAST('<Tran1Time>' AS TIMESTAMP WITH TIME ZONE) ORDER BY Snapshot ID;` |  The result section displays 406 records.   |
 | Retrieve data post-second transaction by using snapshot ID.|`SELECT * FROM iceberg_data.automobiles.cars FOR VERSION AS OF <Tran2SnapshotID> ORDER BY Snapshot ID;` | The result section displays 408 records.   |
 | Retrieve data post-third transaction by using timestamp.| `SELECT * FROM iceberg_data.automobiles.cars FOR TIMESTAMP AS OF CAST('<Tran3Time>' AS TIMESTAMP WITH TIME ZONE) ORDER BY Snapshot ID;`|The result section displays 409 records.   |
 | Retrieve data from a point in time between the second and third transactions.| `SELECT * FROM iceberg_data.automobiles.cars FOR TIMESTAMP AS OF CAST('Choose-a-time-between-<Tran2Time>-and-<Tran3Time>' AS TIMESTAMP WITH TIME ZONE) ORDER BY Snapshot ID;`| The result section displays 408 records.   |
 | Retrieve data from a time before the table was created (expected to fail).| `SELECT * FROM iceberg_data.automobiles.cars FOR TIMESTAMP AS OF CAST('2024-01-01 00:00:00.000 UTC' AS TIMESTAMP WITH TIME ZONE) ORDER BY Snapshot ID;`|No records were found. |
 {: caption="Sample scenarios" caption-side="bottom"}


## Performing table rollback
{: #ingst_stp4}
{: step}

{{site.data.keyword.lakehouse_short}} allows you to rollback a table to an earlier point in time by using snapshots.

To rollback the table data to an earlier snapshot, do the following:

1. Go to **Data manager**.

2. Select the table `cars`. From the **cars** section, select the **Time travel** tab. You can view the snapshot records (with SnapshotID).

5. Click the overflow menu at the end of the row for the second snapshot (the second snapshot includes 408 records) and click **Rollback to snapshot**. A **Confirm rollback to snapshot** window opens. Click **Rollback to snapshot**.
   The data rollback is successful. Now, the table must have 408 records.

2. To verify the rollback, run the following query to check whether the rows corresponding to the third transaction is removed.

   * Sample query to verify that the table does not include the record 'Kia Optima'.

   ```bash
   SELECT * FROM iceberg_data.automobiles.cars WHERE car IN ('Kia Optima', 'Tesla Model S', 'Tesla Model 3');
   ```
   {: codeblock}



   The result lists the data records corresponding to 'Tesla Model S' and 'Tesla Model 3' only. The table does not have the record corresponding to 'Kia Optima' (third transaction) as the table is now rollback to the second snapshot.


   * Sample query to count the total number of rows in the table.

   ```bash
   SELECT COUNT(*) FROM iceberg_data.automobiles.cars;
   ```
   {: codeblock}

   You must see a count of 408 rows, which matches the count when you performed the second transaction in the table. The table is back to its previous (second transaction) state.
