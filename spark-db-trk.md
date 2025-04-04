---

copyright:
  years: 2024
lastupdated: "2025-03-20"
keywords: spark, interface
subcollection: watsonxdata

---

{{site.data.keyword.attribute-definition-list}}

# Track Spark applications
{: #db_trk}

You can track your Spark applications by using Databand through the methods that are mentioned in this section.

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
