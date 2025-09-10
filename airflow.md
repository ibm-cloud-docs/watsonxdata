---

copyright:
  years: 2017, 2025
lastupdated: "2025-09-10"

keywords: watsonx.data, spark, table, maintenance
subcollection: watsonxdata

---

{{site.data.keyword.attribute-definition-list}}

# Orchestration using Apache Airflow
{: #airflow}

Apache Airflow is an open-source platform that enables you to create, schedule, and monitor workflow. Work-flows are defined as Directed Acyclic Graphs (DAGs) which consist of multiple tasks written using Python code. Each task represents a discrete unit of work, such as running a script, querying a database, or calling an API. The Airflow architecture supports scaling and parallel execution, making it suitable for managing complex, data-intensive pipelines.
{: shortdesc}

Apache airflow supports the following use cases :
* ETL or ELT Pipelines : Extracting data from various sources, transforming it, and loading it into the data warehouse.
* Data Warehousing : Scheduling regular updates and data transformations in a data warehouse.
* Data Processing : Orchestrating distributed data processing tasks across different systems.

## Prerequisites
{: #airflw_spk_preq}

* Apache Airflow stand-alone active instance.
* User API keys for watsonx.data (username and api_key). For example, `username`: `yourid@example.com` and `api_key`: `sfw....cv23`.
* CRN for watsonx.data (wxd_instance_id). Get the instance ID from the watsonx.data information page.
* Spark engine id from an active Spark engine (spark_engine_id).
* Presto external url from an active Presto engine (presto_ext_url).
* SSL certificate location which is trusted by the system (if applicable).
* Catalog associated with Spark and Presto engines (catalog_name).
* Name of the bucket associated with the selected catalog. (bucket_name).
* Install the packages, Pandas and Presto-python-client using the command: `pip install pandas presto-python-client`.



## Procedure
{: #airflw_proc}

1. The use case considers a task to ingest data to Presto. To do that, create a Spark application that ingests Iceberg data to the watsonx.data catalog. Here,  the sample Python file ingestion-job.py is considered.

    ``` bash
    from pyspark.sql import SparkSession
    import os, sys

    def init_spark():
        spark = SparkSession.builder.appName("ingestion-demo").enableHiveSupport().getOrCreate()
        return spark

    def create_database(spark,bucket_name,catalog):
        spark.sql("create database if not exists {}.demodb LOCATION 's3a://{}/demodb'".format(catalog,bucket_name))

    def list_databases(spark,catalog):
        # list the database under lakehouse catalog
        spark.sql("show databases from {}".format(catalog)).show()

    def basic_iceberg_table_operations(spark,catalog):
        # demonstration: Create a basic Iceberg table, insert some data and then query table
        print("creating table")
        spark.sql("create table if not exists {}.demodb.testTable(id INTEGER, name VARCHAR(10), age INTEGER, salary DECIMAL(10, 2)) using iceberg".format(catalog)).show()
        print("table created")
        spark.sql("insert into {}.demodb.testTable values(1,'Alan',23,3400.00),(2,'Ben',30,5500.00),(3,'Chen',35,6500.00)".format(catalog))
        print("data inserted")
        spark.sql("select * from {}.demodb.testTable".format(catalog)).show()



    def clean_database(spark,catalog):
        # clean-up the demo database
        spark.sql("drop table if exists {}.demodb.testTable purge".format(catalog))
        spark.sql("drop database if exists {}.demodb cascade".format(catalog))

    def main(wxdDataBucket, wxdDataCatalog):
        try:
            spark = init_spark()

            create_database(spark,wxdDataBucket,wxdDataCatalog)
            list_databases(spark,wxdDataCatalog)
            basic_iceberg_table_operations(spark,wxdDataCatalog)


        finally:
            # clean-up the demo database
            clean_database(spark,wxdDataCatalog)
            spark.stop()

    if __name__ == '__main__':
        main(sys.argv[1],sys.argv[2])

    ```
    {: codeblock}

1. Upload the file to the storage with name, `bucket_name`. For more information, see [Add some objects to your buckets](https://cloud.ibm.com/docs/cloud-object-storage?topic=cloud-object-storage-getting-started-cloud-object-storage#gs-add-objects).

1. Design a DAG workflow using Python and save the Python file to the Apache Airflow directory location, `$AIRFLOW_HOME/dags/` directory (Default value of AIRFLOW_HOME is set to ~/airflow).

    The following is an example of a workflow, which execute tasks to ingest data to Presto in watsonx.data, and query data from watsonx.data.
    Save the file with the following content, as `wxd_pipeline.py`.

    When using the v2 API, set the <api_version> parameter to `v2`; for the v3 API, set it to `v3`.


    ``` bash

    from datetime import timedelta, datetime
    from time import sleep
    import prestodb
    import pandas as pd
    import base64
    import os # type: ignore

    # The DAG object
    from airflow import DAG

    # Operators
    from airflow.operators.python_operator import PythonOperator # type: ignore
    import requests

    # Initializing the default arguments
    default_args = {
        'owner': 'IBM watsonx.data',
        'start_date': datetime(2024, 3, 4),
        'retries': 3,
        'retry_delay': timedelta(minutes=5),
        'wxd_endpoint': 'https://us-south.lakehouse.cloud.ibm.com', # Host endpoint
        'wxd_instance_id': 'crn:...::', # watsonx.data CRN
        'wxd_username': 'yourid@example.com', # your email id
        'wxd_api_key': 'sfw....cv23', # IBM IAM Api Key
        'spark_engine_id': 'spark6', # Spark Engine id
        'catalog_name': 'my_iceberg_catalog', # Catalog name where data will be ingestion
        'bucket_name': 'my-wxd-bucket', # Bucket name (not display name) associated with the above catalog
        'presto_eng_host': '2ce72...d59.cise...5s20.lakehouse.appdomain.cloud', # Presto engine hostname (without protocol and port)
        'presto_eng_port': 30912 # Presto engine port (in numbers only)
    }

    # Instantiate a DAG object
    wxd_pipeline_dag = DAG('wxd_ingestion_pipeline_saas',
            default_args=default_args,
            description='watsonx.data ingestion pipeline',
            schedule_interval=None,
            is_paused_upon_creation=True,
            catchup=False,
            max_active_runs=1,
            tags=['wxd', 'watsonx.data']
    )

    # Workaround: Enable if you want to disable SSL verification
    os.environ['NO_PROXY'] = '*'


    # Get access token
    def get_access_token():
        try:
            url = f"https://iam.cloud.ibm.com/oidc/token"
            headers = {
                'Content-Type': 'application/x-www-form-urlencoded',
                'Accept': 'application/json',
            }

            data = {
                'grant_type': 'urn:ibm:params:oauth:grant-type:apikey',
                'apikey': default_args['wxd_api_key'],
            }


            response = requests.post('https://iam.cloud.ibm.com/identity/token', headers=headers, data=data)

            return response.json()['access_token']
        except Exception as inst:
            print('Error in getting access token')
            print(inst)
            exit


    def _ingest_via_spark_engine():
        try:
            print('ingest__via_spark_engine')
            url = f"{default_args['wxd_endpoint']}/lakehouse/api/<api_version>/spark_engines/{default_args['spark_engine_id']}/applications"

            headers = {'Content-type': 'application/json', 'Authorization': f'Bearer {get_access_token()}', 'AuthInstanceId': default_args['wxd_instance_id']}
            auth_str = base64.b64encode(f'ibmlhapikey_{default_args["wxd_username"]}:{default_args["wxd_api_key"]}'.encode('ascii')).decode("ascii")

            response = requests.post(url, None, {
                "application_details": {
                    "conf": {
                        "spark.executor.cores": "1",
                        "spark.executor.memory": "1G",
                        "spark.driver.cores": "1",
                        "spark.driver.memory": "1G",
                        "spark.hadoop.wxd.apikey": f"Basic {auth_str}"
                    },
                    "application": f"s3a://{default_args['bucket_name']}/ingestion-job.py",
                    "arguments": [
                        default_args['bucket_name'],
                        default_args['catalog_name']
                    ],
                }
            } , headers=headers, verify=False)

            print("Response", response.content)
            return response.json()['id']
        except Exception as inst:
            print(inst)
            raise ValueError('Task failed due to', inst)


    def _wait_until_job_is_complete(**context):
        try:
            print('wait_until_job_is_complete')
            application_id = context['task_instance'].xcom_pull(task_ids='ingest_via_spark_engine')
            print(application_id)

            while True:
                url = f"{default_args['wxd_endpoint']}/lakehouse/api/<api_version>/spark_engines/{default_args['spark_engine_id']}/applications/{application_id}"
                headers = {'Content-type': 'application/json', 'Authorization': f'Bearer {get_access_token()}', 'AuthInstanceId': default_args['wxd_instance_id']}

                response = requests.get(url, headers=headers, verify=False)
                print(response.content)

                data = response.json()

                if data['state'] == 'finished':
                    break
                elif data['state'] in ['stopped', 'failed', 'killed']:
                    raise ValueError("Job failed: ", data)

                print('Job is not completed, sleeping for 10secs')
                sleep(10)
        except Exception as inst:
            print(inst)
            raise ValueError('Task failed due to', inst)


    def _query_presto():
        try:
            with prestodb.dbapi.connect(
                host=default_args['presto_eng_host'],
                port=default_args['presto_eng_port'],
                user=default_args['wxd_username'],
                catalog='tpch',
                schema='tiny',
                http_scheme='https',
                auth=prestodb.auth.BasicAuthentication(f'ibmlhapikey_{default_args["wxd_username"]}', default_args["wxd_api_key"])
            ) as conn:
                df = pd.read_sql_query(f"select * from {default_args['catalog_name']}.demodb.testTable limit 5", conn)

                with pd.option_context('display.max_rows', None, 'display.max_columns', None):
                    print("\n", df.head())
        except Exception as inst:
            print(inst)
            raise ValueError('Query faield due to ', inst)


    def start_job():
        print('Validating default arguments')

        if 'wxd_endpoint' not in default_args:
            raise ValueError('wxd_endpoint is mandatory')

        if 'wxd_username' not in default_args:
            raise ValueError('wxd_username is mandatory')

        if 'wxd_instance_id' not in default_args:
            raise ValueError('wxd_instance_id is mandatory')

        if 'wxd_api_key' not in default_args:
            raise ValueError('wxd_api_key is mandatory')

        if 'spark_engine_id' not in default_args:
            raise ValueError('spark_engine_id is mandatory')


    start = PythonOperator(task_id='start_task', python_callable=start_job, dag=wxd_pipeline_dag)

    ingest_via_spark_engine = PythonOperator(task_id='ingest_via_spark_engine', python_callable=_ingest_via_spark_engine, dag=wxd_pipeline_dag)
    wait_until_ingestion_is_complete = PythonOperator(task_id='wait_until_ingestion_is_complete', python_callable=_wait_until_job_is_complete, dag=wxd_pipeline_dag)
    query_via_presto = PythonOperator(task_id='query_via_presto', python_callable=_query_presto, dag=wxd_pipeline_dag)

    start >> ingest_via_spark_engine >> wait_until_ingestion_is_complete >> query_via_presto

    ```
    {: codeblock}

1. Log in to **Apache Airflow**.
1. Search for `wxd_pipeline.py` job, enable the DAG from **Apache Airflow** console page. The workflow gets executed successfully.
