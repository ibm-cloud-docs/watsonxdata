---

copyright:
  years: 2022, 2024
lastupdated: "2024-02-28"

keywords: watsonx.data, data ingestion, source file

subcollection: watsonxdata

---

{:javascript: #javascript .ph data-hd-programlang='javascript'}
{:java: #java .ph data-hd-programlang='java'}
{:ruby: #ruby .ph data-hd-programlang='ruby'}
{:php: #php .ph data-hd-programlang='php'}
{:python: #python .ph data-hd-programlang='python'}
{:external: target="_blank" .external}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:tip: .tip}
{:important: .important}
{:note: .note}
{:deprecated: .deprecated}
{:pre: .pre}
{:video: .video}

# Spark ingestion through ibm-lh tool command line
{: #ingest_spark_cli}

You can run the **ibm-lh** tool to ingest data into {{site.data.keyword.lakehouse_full}} through the command line interface (CLI) using the IBM Analytics Engine (Spark). The commands to run the ingestion job are listed in this topic.
{: shortdesc}

## Before you begin
{: #byb}

* You must have the Administrator role and privileges in the catalog to do ingestion through the web console.
* Add and register IBM Analytics Engine (Spark). See Registering an engine.
* Add bucket for the target catalog. See Adding a bucket-catalog pair.
* Create schema and table in the catalog for the data to be ingested. See Creating schemas and Creating tables.

## Procedure
{: #procdre}

1. Set the following environment variables before starting an ingestion job by running the following commands:

   ```bash
   export IBM_LH_BEARER_TOKEN=<token>
   export IBM_LH_SPARK_JOB_ENDPOINT=https://<cpd_url>/v4/analytics_engines/<instance_id>/spark_applications
   export HMS_CLIENT_USER=lakehouse
   export HMS_CLIENT_PASSWORD=<instance secret>
   export SOURCE_S3_CREDS=AWS_ACCESS_KEY_ID=*******,AWS_SECRET_ACCESS_KEY=*******,ENDPOINT_URL=<endpoint_url>,AWS_REGION=<region>,BUCKET_NAME=<bucket_name>
   export TARGET_S3_CREDS=AWS_ACCESS_KEY_ID=*******,AWS_SECRET_ACCESS_KEY=*******,ENDPOINT_URL=<endpoint_url>,AWS_REGION=<region>,BUCKET_NAME=<bucket_name>
   export IBM_LH_SPARK_EXECUTOR_CORES=<value>
   export IBM_LH_SPARK_EXECUTOR_MEMORY=<value>
   export IBM_LH_SPARK_EXECUTOR_COUNT=<value>
   export IBM_LH_SPARK_DRIVER_CORES=<value>
   export IBM_LH_SPARK_DRIVER_MEMORY=<value>
   ```
   {: codeblock}

   For IBM Cloud, the Spark driver, executor vCPU and memory combinations must be in a 1:2, 1:4, or 1:8 ratio. See [Default limits and quotas for Analytics Engine instances](https://cloud.ibm.com/docs/AnalyticsEngine?topic=AnalyticsEngine-limits).
   {: note}

   |Environment variable name|Description|
   |-------|-----|
   |IBM_LH_BEARER_TOKEN|Authorization bearer token.|
   |   |CPD: https://cloud.ibm.com/apidocs/cloud-pak-data/cloud-pak-data-4.7.0#getauthorizationtoken|
   |   |SaaS: https://cloud.ibm.com/docs/account?topic=account-iamtoken_from_apikey|
   |IBM_LH_SPARK_JOB_ENDPOINT|Spark applications v4 endpoint for CPD and v3 endpoint for SaaS.|
   |    |Refer to Step 1 in document: https://www.ibm.com/docs/en/cloud-paks/cp-data/4.7.x?topic=administering-managing-instances to retrieve CPD Spark Endpoint|
   |    |To retrieve SaaS Spark Endpoint: https://cloud.ibm.com/docs/AnalyticsEngine?topic=AnalyticsEngine-retrieve-endpoints-serverless|
   |HMS_CLIENT_USER|User for Hive Metastore client. CPD Spark implementation uses lakehouse. SaaS Spark implementation uses ibmlhapikey.|
   |HMS_CLIENT_PASSWORD|Password for Hive Metastore client.|
   |SOURCE_S3_CREDS|S3 credentials for the source file bucket in the format:`“AWS_ACCESS_KEY_ID=<access_key>,AWS_SECRET_ACCESS_KEY=<secret_key>,ENDPOINT_URL=<endpoint_url>,AWS_REGION=<region>,BUCKET_NAME=<bucket_name>”`|
   |TARGET_S3_CREDS|S3 credentials for the target table bucket in the format: `“AWS_ACCESS_KEY_ID=<access_key>,AWS_SECRET_ACCESS_KEY=<secret_key>,ENDPOINT_URL=<endpoint_url>,AWS_REGION=<region>,BUCKET_NAME=<bucket_name>”`|
   |IBM_LH_SPARK_EXECUTOR_CORES|Optional spark engine configuration setting for executor cores|
   |IBM_LH_SPARK_EXECUTOR_MEMORY|Optional spark engine configuration setting for executor memory|
   |IBM_LH_SPARK_EXECUTOR_COUNT|Optional spark engine configuration setting for executor count|
   |IBM_LH_SPARK_DRIVER_CORES|Optional spark engine configuration setting for driver cores|
   |IBM_LH_SPARK_DRIVER_MEMORY|Optional spark engine configuration setting for driver memory|
   {: caption="Table 1" caption-side="bottom"}

2. Run the following command to ingest data:

   ```bash
   ibm-lh data-copy --source-data-files s3://path/to/file/or/folder \
   --target-tables <catalog>.<schema>.<table> \
   --ingestion-engine-endpoint "hostname=<hostname>,port=<port>,type=spark" \
   --trust-store-password <truststore password> \
   --trust-store-path <truststore path> \
   --target-catalog-uri 'thrift://<hms_thrift_uri>'
   ```
   {: codeblock}

   |Parameter|Description|
   |------------|----------|
   |--source-data-files|Path to s3 parquet or CSV file or folder. Folder paths must end with “/”|
   |--target-tables|Target table in format `<catalog>.<schema>.<table>`. Catalog name will be the name of the spark catalog that will be initiated. Schema should be pre-existent. Table name will be the table to insert into or create.|
   |--ingestion-engine-endpoint|Ingestion engine endpoint will be in the format hostname=’’,port=’’,type=spark”. Type is required to be set to spark.|
   |--trust-store-password|Password of the truststore cert inside the spark job pod. Current implementation of Spark for CPD and SaaS requires: changeit|
   |--trust-store-path|Path of the truststore cert inside the spark job pod. Current implementation of Spark for CPD and SaaS requires: file:///opt/ibm/jdk/lib/security/cacerts|
   |--target-catalog-uri|HMS thrift endpoint.|
   |    |CPD endpoint example: `thrift://ibm-lh-lakehouse-hive-metastore-svc.cpd-instance.svc.cluster.local:9083`|
   |    |SaaS endpoint example: `thrift://<identifier>.<identifier>.lakehouse.dev.appdomain.cloud:31894`.
   |--create-if-not-exist|Pass in this option if the target table is not created and the tool should create it. Do not pass in this option if the target table is already created and the tool should insert into that table.|
   |--schema|Pass in this option with value in the format path/to/csvschema/config/file. Pass in the path to a schema.cfg file which specifies header and delimiter values for CSV source file or folder.|
   {: caption="Table 2" caption-side="bottom"}


## Limitations
{: #limits}

Following are some of the limitations of Spark ingestion:

- Spark ingestion supports only source data files from object storage bucket. Local files are not supported.
- The default buckets in watsonx.data are not exposed to Spark engine. Hence, iceberg-bucket and hive-bucket are not supported for source or target table. Users can use their own MinIo or S3 compatible buckets that are exposed and accessible by Spark engine.
- Source files must be a single file or folder of files with same data type and the data is of same ddl.
- Advanced table customization for CSV files supports only header and field delimiter. Customization for encoding value, line delimiter and escape character is ignored and default values are considered. Default values are as follows:

   - Encoding value: UTF-8

   - Escape character: \\\

   - Line delimiter: \n
