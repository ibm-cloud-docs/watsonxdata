---

copyright:
  years: 2022, 2025
lastupdated: "2025-11-06"

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

# Spark ingestion through ibm-lh tool
{: #ingest_spark_cli}

You can run the **ibm-lh** tool to ingest data into {{site.data.keyword.lakehouse_full}} through the command line interface (CLI) using the IBM Analytics Engine (Spark). The commands to run the ingestion job are listed in this topic.
{: shortdesc}

## Before you begin
{: #byblegsprk}

* You must have the **Administrator** role and privileges in the catalog to do ingestion through the web console.
* Add and register IBM Analytics Engine (Spark). See [Provisioning a Spark engine]({{site.data.keyword.ref-spl_engine-link}}).
* Add storage for the target catalog. See [Adding a storage]({{site.data.keyword.ref-reg_bucket-link}}).
* Create schema and table in the catalog for the data to be ingested. See [Creating schemas]({{site.data.keyword.ref-create_schema-link}}) and [Creating tables]({{site.data.keyword.ref-create_table-link}}).

## Procedure
{: #procdre}

1. Set the mandatory environment variable `ENABLED_INGEST_MODE` to `SPARK_LEGACY` before starting an ingestion job by running the following command:

   Starting with {{site.data.keyword.lakehouse_short}} version 2.2.0, authentication using `ibmlhapikey` and `ibmlhtoken` as usernames is deprecated. These formats will be phased out in a future release. To ensure compatibility with upcoming versions, use the new format:`ibmlhapikey_<username>` and `ibmlhtoken_<username>`.
   {: important}

   ```bash
   export ENABLED_INGEST_MODE=SPARK_LEGACY
   ```
   {: codeblock}

1. Set the following environment variables before starting an ingestion job by running the following commands:

   ```bash
   export IBM_LH_BEARER_TOKEN=<token>
   export IBM_LH_SPARK_JOB_ENDPOINT=https://<cpd_url>/v4/analytics_engines/<instance_id>/spark_applications
   export HMS_CLIENT_USER=lakehouse
   export HMS_CLIENT_PASSWORD=<instance secret>
   export SOURCE_S3_CREDS="AWS_ACCESS_KEY_ID=*******,AWS_SECRET_ACCESS_KEY=*******,ENDPOINT_URL=<endpoint_url>,AWS_REGION=<region>,BUCKET_NAME=<bucket_name>"
   export TARGET_S3_CREDS="AWS_ACCESS_KEY_ID=*******,AWS_SECRET_ACCESS_KEY=*******,ENDPOINT_URL=<endpoint_url>,AWS_REGION=<region>,BUCKET_NAME=<bucket_name>"
   export IBM_LH_SPARK_EXECUTOR_CORES=<value>
   export IBM_LH_SPARK_EXECUTOR_MEMORY=<value>
   export IBM_LH_SPARK_EXECUTOR_COUNT=<value>
   export IBM_LH_SPARK_DRIVER_CORES=<value>
   export IBM_LH_SPARK_DRIVER_MEMORY=<value>
   export INSTANCE_ID=<instance_id>
   export USE_NATIVE_SPARK=<true/false>
   export USE_EXTERNAL_SPARK=<true/false>
   export IBM_LH_URL=https://<lh_hostname>
   export IBM_LH_USER_BEARER_TOKEN=<token>
   ```
   {: codeblock}

   If IBM Analytics Engine Serverless instance on IBM Cloud is registered as external Spark on {{site.data.keyword.lakehouse_short}}, the Spark driver, executor vCPU and memory combinations must be in a 1:2, 1:4, or 1:8 ratio. See [Default limits and quotas for Analytics Engine instances](https://cloud.ibm.com/docs/AnalyticsEngine?topic=AnalyticsEngine-limits).
   {: note}

   |Environment variable name|Description|
   |-------|-----|
   |`IBM_LH_BEARER_TOKEN`|Authorization bearer token. For more information, see https://cloud.ibm.com/docs/account?topic=account-iamtoken_from_apikey. For `USE_EXTERNAL_SPARK=true`, the bearer token should be generated with external Spark engine API key.|
   |`IBM_LH_SPARK_JOB_ENDPOINT`|Spark applications v4 endpoint for CPD and v3 endpoint for SaaS. To retrieve SaaS Spark Endpoint: https://cloud.ibm.com/docs/AnalyticsEngine?topic=AnalyticsEngine-retrieve-endpoints-serverless|
   |`HMS_CLIENT_USER`|User for Metadata Service client. SaaS Spark implementation uses `ibmlhapikey`.|
   |`HMS_CLIENT_PASSWORD`|Password for Metadata Service client. For SaaS, you can use the API key named `ibmlhapikey` from the cloud account where {{site.data.keyword.lakehouse_short}} has been deployed.|
   |`SOURCE_S3_CREDS`|S3 credentials for the source file storage in the format:`“AWS_ACCESS_KEY_ID=<access_key>,AWS_SECRET_ACCESS_KEY=<secret_key>,ENDPOINT_URL=<endpoint_url>,AWS_REGION=<region>,BUCKET_NAME=<bucket_name>”`|
   |`TARGET_S3_CREDS`|S3 credentials for the target table storage in the format: `“AWS_ACCESS_KEY_ID=<access_key>,AWS_SECRET_ACCESS_KEY=<secret_key>,ENDPOINT_URL=<endpoint_url>,AWS_REGION=<region>,BUCKET_NAME=<bucket_name>”`|
   |`IBM_LH_SPARK_EXECUTOR_CORES`|Optional spark engine configuration setting for executor cores.|
   |`IBM_LH_SPARK_EXECUTOR_MEMORY`|Optional spark engine configuration setting for executor memory.|
   |`IBM_LH_SPARK_EXECUTOR_COUNT`|Optional spark engine configuration setting for executor count.|
   |`IBM_LH_SPARK_DRIVER_CORES`|Optional spark engine configuration setting for driver cores.|
   |`IBM_LH_SPARK_DRIVER_MEMORY`|Optional spark engine configuration setting for driver memory.|
   |`INSTANCE_ID`|Identify unique instances. In SaaS environment, CRN is the instance id. This is a mandatory parameter.|
   |`USE_NATIVE_SPARK`|When native spark is used for ingestion, this parameter value must be `true`. This is a mandatory parameter.|
   |`USE_EXTERNAL_SPARK`|When external spark is used for ingestion, this parameter value must be `true`.|
   |`IBM_LH_URL`|This parameter is used only when `USE_EXTERNAL_SPARK=true`. The value is `https://<lh_hostname>`. `<lh_hostname>` is the hostname of {{site.data.keyword.lakehouse_short}} instance.|
   |`IBM_LH_USER_BEARER_TOKEN`|This parameter is used only when `USE_EXTERNAL_SPARK=true`. The bearer token should be generated with User API key. For more information, see https://cloud.ibm.com/docs/account?topic=account-iamtoken_from_apikey.|
   {: caption="Table 1" caption-side="bottom"}

2. You can run ingestion jobs to ingest data in 2 ways, using a simple command line or a config file.

   1. Run the following command to ingest data from a single or multiple source data files:

      ```bash
      ibm-lh data-copy --source-data-files s3://path/to/file/or/folder \
      --target-table <catalog>.<schema>.<table> \
      --ingestion-engine-endpoint "hostname=<hostname>,port=<port>,type=spark" \
      --trust-store-password <truststore password> \
      --trust-store-path <truststore path> \
      --log-directory /tmp/mylogs \
      --partition-by "<columnname1>, <columnname2> \
      --target-catalog-uri 'thrift://<mds_thrift_uri>'
      ```
      {: codeblock}

      Where the parameters used are listed as follows:

      |Parameter|Description|
      |------------|----------|
      |`--source-data-files`|Path to s3 parquet or CSV file or folder. Folder paths must end with “/”. File names are case sensitive.|
      |`--target-table`|Target table in format `<catalogname>.<schemaname>.<tablename>`.|
      |`--log-directory`|This option is used to specify the location of log files.|
      |`--ingestion-engine-endpoint`|Ingestion engine endpoint will be in the format `hostname=’’,port=’’,type=spark”`. Type must be set to spark.|
      |`--partition-by`|This parameter supports the functions for years, months, days, hours for timestamp in the `partition-by` list. If a target table already exist or the `create-if-not-exist` parameter is not mentioned the partition-by shall not make any effect on the data.|
      |`--trust-store-password`|Password of the truststore certificate inside the spark job pod. Current password for Spark in CPD and SaaS is `changeit`.|
      |`--trust-store-path`|Path of the truststore cert inside the spark job pod. Current path of Spark in CPD and SaaS is `file:///opt/ibm/jdk/lib/security/cacerts`.|
      |`--target-catalog-uri`|MDS thrift endpoint.|
      |    |SaaS endpoint example: `thrift://<metastore_host_value>`. `<metastore_host_value>` is taken from the details tab of the catalog in the Infrastructure page.|
      |`--create-if-not-exist`|Use this option if the target schema or table is not created. Do not use if the target schema or table is already created.|
      |`--schema`|Use this option with value in the format path/to/csvschema/config/file. Use the path to a schema.cfg file which specifies header and delimiter values for CSV source file or folder.|
      {: caption="Table 2" caption-side="bottom"}

   2. Run the following command to ingest data from a config file:

      ```bash
      ibm-lh data-copy --ingest-config /<your_ingest_configfilename>
      ```
      {: codeblock}

      Where the config file has the following information:
      ```bash
      [global-ingest-config]
      target-tables:<catalog>.<schema>.<table>
      ingestion-engine:hostname='',port='',type=spark
      create-if-not-exist:true/false

      [ingest-config1]
      source-files:s3://path/to/file/or/folder
      target-catalog-uri:thrift://<mds_thrift_uri>
      trust-store-path:<truststore path>
      trust-store-password:<truststore password>
      log-directory /tmp/mylogs
      partition-by "<columnname1>, <columnname2>
      schema:/path/to/csvschema/config/file [Optional]
      ```
      {: codeblock}

      The parameters used in the config file ingestion job is listed as follows:

      |Parameter|Description|
      |------------|----------|
      |`source-files`|Path to s3 parquet or CSV file or folder. Folder paths must end with “/”|
      |`target-table`|Target table in format `<catalogname>.<schemaname>.<tablename>`.|
      |`ingestion-engine`|Ingestion engine endpoint will be in the format `hostname=’’, port=’’,type=spark”`. Type must be set to spark.|
      |`log-directory`|This option is used to specify the location of log files.|
      |`--partition-by`|This parameter supports the functions for years, months, days, hours for timestamp in the `partition-by` list. If a target table already exist or the `create-if-not-exist` parameter is not mentioned the partition-by shall not make any effect on the data.|
      |`trust-store-password`|Password of the truststore certificate inside the spark job pod. Current password for Spark in CPD and SaaS is `changeit`.|
      |`trust-store-path`|Path of the truststore cert inside the spark job pod. Current path of Spark in CPD and SaaS is `file:///opt/ibm/jdk/lib/security/cacerts`.|
      |`target-catalog-uri`|MDS thrift endpoint.|
      |    |CPD endpoint example: `thrift://<metastore_host_value>`. `<metastore_host_value>` is taken from the details tab of the catalog in the Infrastructure page.|
      |    |SaaS endpoint example: `thrift://<metastore_host_value>`. `<metastore_host_value>` is taken from the details tab of the catalog in the Infrastructure page.|
      |`create-if-not-exist`|Use this option if the target schema or table is not created. Do not use if the target schema or table is already created.|
      |`schema`|Use this option with value in the format path/to/csvschema/config/file. Use the path to a schema.cfg file which specifies header and delimiter values for CSV source file or folder.|
      {: caption="Table 3" caption-side="bottom"}

   The ability to handle special characters in table and schema names for ingestion is constrained by the underlying engines (Spark, Presto) and their respective special character support.

   - Regular syntax: `--target-tables <catalogname>.<schemaname>.<tablename>`.
   - Syntax with special character option 1: `--target-tables <catalogname>.<schemaname>."table\.name"`. Using this syntax, escape character `\` is used within double quotes to escape period(.). Escape character `\` is used only when special character period(.) is in the table name.
   - Syntax with special character option 2: `--target-tables <catalogname>.<schemaname>."'table.name'"`. Using this syntax, period(.) is not escaped nor need to use the escape character when using additional single quotes.
