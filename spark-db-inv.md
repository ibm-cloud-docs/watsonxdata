---

copyright:
  years: 2024
lastupdated: "2024-09-13"
keywords: spark, interface
subcollection: watsonxdata

---

{{site.data.keyword.attribute-definition-list}}

# Invoke Spark applications
{: #db_inv}

This section provides examples of submitting your Spark application while integrating Databand.

## End-to-End Example of using Databand listener
{: #db_inv_e2e}

Your PySpark script can benefit from automatic tracking of data set operations without requiring any code changes.

1. Create a JSON file for submitting your Spark job as follows. Example: `submit-application.son`.

   ```json
   {
     "application_details": {
       "application": "s3a://<s3_bucket_name>/<application_name>.py",
       "jars": "s3a://<s3_bucket_name>/dbnd-agent-<version>-all.jar",
       "conf": {
         "spark.hadoop.fs.s3a.bucket.<s3_bucket_name>.endpoint": "<s3a_endpoint>",
         "spark.hadoop.fs.s3a.bucket.<s3_bucket_name>.access.key": "<s3 bucket HMAC access key>",
         "spark.hadoop.fs.s3a.bucket.<s3_bucket_name>.secret.key": "<s3 bucket  HMAC secret key>",
         "spark.app.name": "<app_name>",
         "spark.sql.queryExecutionListeners": "ai.databand.spark.DbndSparkQueryExecutionListener"
       },
       "env": {
         "DBND__CORE__DATABAND_URL": "<Databand Server url>",
         "DBND__CORE__DATABAND_ACCESS_TOKEN": "Personal access token for your account",
         "DBND__TRACKING": "True",
         "DBND__ENABLE__SPARK_CONTEXT_ENV": "True",
         "DBND__TRACKING__PROJECT": "<project_name_for_your_Databand_pipeline>",
         "DBND__TRACKING__JOB": "<pipeline_name_for_your_Databand_run>",
         "DBND__RUN_INFO__NAME": "<run_name>"
       }
     }
   }
   ```
   {: codeblock}

   Properties for enabling Databand features are passed as Spark environment variables:

   - `spark.sql.queryExecutionListeners`: Used to register a custom listener that is provided by DataBand for Spark SQL query executions. This listener integrates with Spark to collect and report metrics or information about query executions.
   - `DBND__CORE__DATABAND_URL`: The URL for accessing your Databand instance (for example, yourcompanyname.databand.ai).
   - `DBND__CORE__DATABAND_ACCESS_TOKEN`: Your Databand Access Token that is used for connecting to the environment.
   - `DBND__TRACKING` : Controls whether tracking is enabled or disabled for the project.
   - `DBND__ENABLE__SPARK_CONTEXT_ENV`: Activates implicit tracking within the Spark context.
   - `DBND__TRACKING__PROJECT`: Specifies the project name for tracking.
   - `DBND__TRACKING__JOB`: Specifies the job name for tracking.
   - `DBND__RUN_INFO__NAME`: Specifies run names that are displayed in the Databand UI.
   - `dbnd-agent jar`: Store this jar in any accessible S3 location. If using an agent, Databand listeners are activated automatically as the agent’s `FatJar` (`-all.jar` file) includes all necessary Databand code. Download the latest version from the [Maven Repository](https://repo1.maven.org/maven2/ai/databand/dbnd-agent/).

   You can add more configuration properties as required as listed in [Databand Configuration](https://www.ibm.com/docs/en/dobd?topic=applications-installing-jvm-sdk-agent#configuration).

1. Submit the Spark application by using the following curl command.

   ```bash
   curl --request POST \
     --url https://<region>.lakehouse.cloud.ibm.com/lakehouse/api/v2/spark_engines/<spark_engine_id>/applications \
     --header 'Authorization: Bearer <token>' \
     --header 'Content-Type: application/json' \
     --header 'AuthInstanceID: <crn_instance>' \
     --data @submit-application.json
     ```
     {: codeblock}

    For more information, see [Submit engine applications](watsonxdata?topic=watsonxdata-smbit_nsp_1).

After you submit the Spark application, you will receive a confirmation message with the application ID and Spark version. Keep this information for tracking the execution status of your submitted Spark job. You can monitor and track datasets by using Databand's tracking features within the Databand environment.

## End-to-End example of using Databand APIs
{: #db_inv_e2e_api}

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


To submit a Spark job, do the following steps:

1. Prepare a sample json file, example: `submit-application.json`.

   ```json
   {
     "application_details": {
       "conf": {
         "spark.hadoop.fs.s3a.bucket.<s3_bucket_name>.endpoint": "<s3a_endpoint>",
         "spark.hadoop.fs.s3a.bucket.<s3_bucket_name>.access.key": "<s3_bucket_HMAC_access_key>",
         "spark.hadoop.fs.s3a.bucket.<s3_bucket_name>.secret.key": "<s3_bucket_HMAC_secret_key>",
         "ae.spark.librarysets": "dbnd-lib"
       },
       "env": {
         "DBND__CORE__DATABAND_URL": "<Databand Server url>",
         "DBND__CORE__DATABAND_ACCESS_TOKEN": "Personal access token for your account",
         "DBND__TRACKING": "True",
         "DBND__ENABLE__SPARK_CONTEXT_ENV": "True",
         "DBND__TRACKING__PROJECT": "<project_name_for_your_Databand_pipeline>",
         "DBND__TRACKING__JOB": "<pipeline_name_for_your_Databand_run>",
         "DBND__RUN_INFO__NAME": "<run_name>"
       },
       "application": "s3a://<s3_bucket_name>/<application_name>.py"
     }
   }
   ```
   {: codeblock}

   Here, `dbnd-lib` represents the library set that was been installed.

1. Submit the Spark application by using the following curl command:

   ```bash
   curl --request POST \
     --url https://<region>.lakehouse.cloud.ibm.com/lakehouse/api/v2/spark_engines/<spark_engine_id>/applications \
     --header 'Authorization: Bearer <token>' \
     --header 'Content-Type: application/json' \
     --header 'AuthInstanceID: <crn_instance>' \
     --data @submit-application.json
   ```
   {: codeblock}

   - **region**: The region where the Spark instance is provisioned.
   - **<spark_engine_id>**: The Engine ID of the native Spark engine.
   - **token**: The bearer token. For more information about generating the token, see Generating a bearer token.
   - **<crn_instance>**: The CRN of the watsonx.data instance.
   - **<bucket_name>**: The name of the object storage. Object storage can be Amazon S3, Ceph, Hadoop Distributed File System (HDFS), or IBM Cloud Object Storage (COS). For more information, see Adding a storage-catalog pair.
   - **<s3a_endpoint>**: The direct endpoint of the Object Storage bucket. For example, s3.direct.us-south.cloud-object-storage.appdomain.cloud.
   - **<bucket_HMAC_access_key>**: The access key for object storage. For more information, see Create HMAC credentials by using the CLI.
   - **<bucket_HMAC_secret_key>**: The secret key for object storage. For more information, see Create HMAC credentials by using the CLI.

For more information and examples, see:

- [IBM Data Observability by Databand](https://www.ibm.com/docs/en/dobd?topic=getting-started)
- For PySpark Applications: [Tracking PySpark](https://www.ibm.com/docs/en/dobd?topic=applications-tracking-pyspark)
- For Spark(Java/Scala): [Tracking Spark(Scala/Java)](https://www.ibm.com/docs/en/dobd?topic=applications-tracking-spark-scalajava)
