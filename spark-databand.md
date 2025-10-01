---

copyright:
  years: 2024, 2025
lastupdated: "2025-10-01"
keywords: spark, interface
subcollection: watsonxdata

---

{{site.data.keyword.attribute-definition-list}}

# Monitoring Spark application runs by using Databand
{: #mntr_dband}

**Applies to** : [Spark engine]{: tag-blue}


Databand integration with Spark enhances monitoring capabilities by providing insights that extend beyond Spark UI and Spark History.

Databand improves Spark application monitoring by the following:

- **Advanced monitoring**: Databand’s task annotations enable you to tag and track crucial stages of your Spark application, offering a more meaningful level of monitoring compared to Spark jobs, stages, or tasks.
- **Dataset tracking**: Databand monitors the datasets that are accessed and modified during your Spark application run, providing enhanced visibility into your data flows.
- **Custom alerts**: You can configure alerts for specific stages of your application or track key dataset metrics, allowing you to identify and address potential issues early.

To get started with Databand, you must have an active Databand subscription. You can obtain this by either requesting a Databand cloud application (SaaS) instance, which is deployed by the Databand team, or by opting for a self-hosted (on-premises) installation. For integrating databand with your {{site.data.keyword.lakehouse_short}} instance, you must have the following credentials:

- **Environment address**: The URL for your Databand environment (example: yourcompanyname.databand.ai).
- **Access token**: A Databand access token that is needed to connect to the environment. You can generate and manage tokens through the Databand UI as required. For more details, visit: [Managing personal access tokens](https://www.ibm.com/docs/en/dobd?topic=tokens-managing-personal-access).

## Procedure
{: #steps}

1. Log in to the {{site.data.keyword.lakehouse_short}} console.
1. From the navigation menu, go to **Configurations** > **IBM Data Observability by Databand**.
1. Enter the environment address in the **URL** field and the access token in the **Access token** field.
1. Click **Test connection** to validate the connection.
1. Click **Save** to save the details. You can edit the details by clicking **Edit**.

Databand takes effect for new Spark jobs that are started after enabling it. Previous and ongoing jobs are not recorded for analysis.
{: note}

## Databand listener
{: #db_listen}

This method automatically tracks dataset operations. Your Spark script can benefit from automatic tracking of dataset operations.

## Databand decorators and logging API
{: #db_api1}

To use this method, you must import the `dbnd` module, which requires code modifications.

### End-to-end example of using Databand APIs
{: #db_api}

The following example demonstrates the use of `dbnd` APIs.

**example.py***

```bash
import time
import logging
from pyspark.sql import SparkSession
from pyspark.sql.functions import col
from dbnd import dbnd_tracking, task, dataset_op_logger, log_metric, log_dataframe

# Initialize Spark session
spark = SparkSession.builder \
    .appName("Data Pipeline with Databand") \
    .getOrCreate()

logging.basicConfig(level=logging.INFO)
logger = logging.getLogger(__name__)

@task
def create_sample_data():
    # Create a DataFrame with sample data including columns to be dropped
    data = [
        ("John", "Camping Equipment", 500, "Regular", "USA"),
        ("Jane", "Golf Equipment", 300, "Premium", "UK"),
        ("Mike", "Camping Equipment", 450, "Regular", "USA"),
        ("Emily", "Golf Equipment", 350, "Premium", "Canada"),
        ("Anna", "Camping Equipment", 600, "Regular", "USA"),
        ("Tom", "Golf Equipment", 200, "Regular", "UK")
    ]
    columns = ["Name", "Product line", "Sales", "Customer Type", "Country"]
    retailData = spark.createDataFrame(data, columns)

    # Log the data creation
    unique_file_name = "sample-data"
    with dataset_op_logger(unique_file_name, "read", with_schema=True, with_preview=True, with_stats=True) as logger:
        logger.set(data=retailData)

    return retailData

@task
def filter_data(rawData):
    # Define columns to drop
    columns_to_drop = ['Customer Type', 'Country']

    # Drop the specified columns in PySpark DataFrame
    filteredRetailData = rawData.drop(*columns_to_drop)

    # Log the data after dropping columns
    unique_file_name = 'script://Weekly_Sales/Filtered_df'
    with dataset_op_logger(unique_file_name, "read", with_schema=True, with_preview=True) as logger:
        logger.set(data=filteredRetailData)

    return filteredRetailData

@task
def write_data_by_product_line(filteredData):
    # Filter data for Camping Equipment and write to CSV
    campingEquipment = filteredData.filter(col('Product line') == 'Camping Equipment')
    campingEquipment.write.csv("Camping_Equipment.csv", header=True, mode="overwrite")

    # Log writing the Camping Equipment CSV
    log_dataframe("camping_equipment", campingEquipment, with_schema=True, with_stats=True)

    # Filter data for Golf Equipment and write to CSV
    golfEquipment = filteredData.filter(col('Product line') == 'Golf Equipment')
    golfEquipment.write.csv("Golf_Equipment.csv", header=True, mode="overwrite")

    # Log writing the Golf Equipment CSV
    log_dataframe("golf_equipment", golfEquipment, with_schema=True, with_stats=True)

def prepare_retail_data():
    with dbnd_tracking(
            conf={
                "tracking": {
                    "track_source_code": True
                },
                "log": {
                    "preview_head_bytes": 15360,
                    "preview_tail_bytes": 15360
                }
            }
    ):

        logger.info("Running Databand spark application!")

        start_time_milliseconds = int(round(time.time() * 1000))
        log_metric("metric_check", "OK")

        # Call the step job - create sample data
        rawData = create_sample_data()

        # Filter data
        filteredData = filter_data(rawData)

        # Write data by product line
        write_data_by_product_line(filteredData)

        end_time_milliseconds = int(round(time.time() * 1000))
        elapsed_time = end_time_milliseconds - start_time_milliseconds

        log_metric('elapsed-time', elapsed_time)

        logger.info(f"Total pipeline running time: {elapsed_time:.2f} milliseconds")
        logger.info("Spark execution completed..")

        log_metric("is-success", "OK")

# Invoke the main function
prepare_retail_data()
```
{: codeblock}

Brief Overview of Databand APIs and Features used:

- `dbnd_tracking`: Initializes tracking for your pipeline or application, configuring Databand settings and logging execution details.
   Usage:

   ```bash
   with dbnd_tracking(conf={...}, job_name="job_name", run_name="run_name"):
    # Pipeline code
   ```
   {: codeblock}

- `task`: Marks a function as a Databand task, enabling tracking and monitoring of individual steps in your pipeline.

   Usage:

   ```bash
   @task
   def my_task_function():
   ```
   {: codeblock}

- `dataset_op_logger`: Logs operations on datasets, including schema and statistics.

   Usage:

   ```bash
      with dataset_op_logger(dataset_name, operation_type) as logger:
          logger.set(data=my_dataframe)
   ```
   {: codeblock}

- `log_metric`: Records custom metrics to track performance or other quantitative data during execution.

   Usage:

   ```bash
   log_metric("metric_name", metric_value)
   ```
   {: codeblock}

- `log_dataframe`: Logs details about a DataFrame, such as schema and statistics, for monitoring data transformations.

   Usage:

   ```bash
   log_dataframe("dataframe_name", my_dataframe, with_schema=True, with_stats=True)
   ```
   {: codeblock}

For information about submitting Spark jobs, see [Submit engine applications](https://cloud.ibm.com/apidocs/watsonxdata#create-spark-engine-application).

After you submit the Spark application, you will receive a confirmation message with the application ID and Spark version. Keep this information for tracking the execution status of your submitted Spark job. You can monitor and track datasets by using Databand's tracking features within the Databand environment.

To view the Databand dashboard for tracking, go to **Configurations** > **IBM Data Observability by Databand** and click **View Databand**.

For more information and examples, see:

- [IBM Data Observability by Databand](https://www.ibm.com/docs/en/dobd?topic=getting-started)
- For PySpark Applications: [Tracking PySpark](https://www.ibm.com/docs/en/dobd?topic=applications-tracking-pyspark)
- For Spark(Java/Scala): [Tracking Spark(Scala/Java)](https://www.ibm.com/docs/en/dobd?topic=applications-tracking-spark-scalajava)
