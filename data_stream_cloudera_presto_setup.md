---

copyright:
  years: 2022, 2026
lastupdated: "2026-04-30"

keywords: lakehouse, remote data, cloudera, {{site.data.keyword.lakehouse_short}}

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

# Setting up Cloudera integration with Presto engine
{: #data_stream_cloudera_presto_setup}

## About this task
{: #data_stream_cloudera_presto_setup1}

You can configure {{site.data.keyword.lakehouse_full}} to query Hive tables stored in Cloudera HDFS using the Presto engine through zero-copy data federation. This guide covers the setup process for both Kerberos and non-Kerberos authentication methods.

For general information about Cloudera integration, see [Integrating Cloudera in {{site.data.keyword.lakehouse_short}}](/docs/watsonxdata?topic=watsonxdata-data_stream_cloudera1).

## Before you begin
{: #data_stream_cloudera_presto_setup2}

Ensure that the following prerequisites are met before proceeding.

**Cloudera requirements:**

- An active Cloudera cluster with HDFS
- Access to Cloudera Query Workspace
- Network connectivity between {{site.data.keyword.lakehouse_short}} and Cloudera cluster
- HDFS NameNode hostname and port
- Hive Metastore URI (format: `thrift://<metastore-host>:<port>`)
- Download the required configuration files:
   1. Log in to Cloudera Manager.
   2. Navigate to **Clusters**.
   3. Select **HDFS** from the list.
   4. Click on **Actions**.
   5. Choose **Download Client Configuration** from the dropdown menu.

**Authentication requirements:**

Choose one of the following authentication methods:

- **Non-Kerberos authentication:**
   - HDFS configuration files (`core-site.xml`, `hdfs-site.xml`)
   - HDFS user with appropriate permissions

- **Kerberos authentication:**
   - Kerberos principal and keytab file
   - Kerberos configuration file (`krb5.conf`)
   - HDFS configuration files (`core-site.xml`, `hdfs-site.xml`)
   - Access to Cloudera cluster's Kerberos realm

**{{site.data.keyword.lakehouse_short}} requirements:**

- A provisioned {{site.data.keyword.lakehouse_short}} Presto engine
- Access to Infrastructure Manager with appropriate permissions

## Procedure
{: #data_stream_cloudera_presto_setup3}

1. Create Hive tables directly in Cloudera using the Hue editor querying tables in {{site.data.keyword.lakehouse_short}}.

   1. Log in to Cloudera Hue interface.
   2. Navigate to Hive editor from the left menu.
   3. Create a new database or use an existing one.

      ```sql
      CREATE DATABASE IF NOT EXISTS <database_name>;
      USE <database_name>;
      ```
      {: codeblock}

   4. Create a Hive table with desired schema.

      ```sql
      CREATE TABLE <database_name>.<table_name> (
          id INT,
          name STRING,
          department STRING,
          salary DECIMAL(10,2)
      )
      STORED AS PARQUET
      LOCATION '/user/hive/warehouse/<database_name>.db.<table_name>';
      ```
      {: codeblock}

   5. Insert data into the table.

      ```sql
      INSERT INTO <database_name>.<table_name> VALUES
          (1, 'John Doe', 'IT', 75000),
          (2, 'Jane Smith', 'HR', 65000),
          (3, 'Bob Johnson', 'Finance', 80000);
      ```
      {: codeblock}

   6. Query the table to verify the data inserted in the table.

      ```sql
      SELECT * FROM <database_name>.<table_name>;
      ```
      {: codeblock}

2. Create HDFS storage component in {{site.data.keyword.lakehouse_short}}.

   1. Log in to {{site.data.keyword.lakehouse_short}} console.
   2. Navigate to **Infrastructure Manager** from the left sidebar.
   3. Click **Add Component** button in top right corner.
   4. Select **HDFS** as Component Type.
   5. Provide a **Display Name** for the component.
   6. Enter **HDFS URI** in format: `hdfs://<namenode-host>:<port>`
      - Example: `hdfs://namenode.example.com:8020`
   7. Enter **Hive Metastore URI** in format: `thrift://<metastore-host>:<port>`
      - Example: `thrift://metastore.example.com:9083`
   8. Select **Authentication Type**:
      - **For Non-Kerberos authentication:** Select **Non-Kerberos** and provide **HDFS User** (e.g., `hdfs`, `hive`).
      - **For Kerberos authentication:** Select **Kerberos** and provide:
         - **Kerberos Principal** in format: `<principal>@<REALM>` (Example: `hive/hostname@EXAMPLE.COM`)
         - **Kerberos Realm** (e.g., `EXAMPLE.COM`)
   9. Upload configuration files:
      - **For Non-Kerberos authentication:**
         1. Click **Upload Configuration Files**.
         2. Upload `core-site.xml`.
         3. Upload `hdfs-site.xml`.
         4. Verify files are uploaded successfully.

      - **For Kerberos authentication:**
         1. Upload the following files in order:
            - `core-site.xml` - HDFS core configuration
            - `hdfs-site.xml` - HDFS site configuration
            - `krb5.conf` - Kerberos configuration
            - Keytab File - Kerberos authentication credentials
         2. Ensure all four files are uploaded successfully before proceeding.

      Ensure all required files are uploaded successfully before proceeding.
      {: important}

   10. Click **Test Connection** button.
   11. Wait for validation to complete (Kerberos authentication validation if applicable).
   12. Verify success message appears.

      If connection fails:
      - Verify HDFS URI and Hive Metastore URI are correct
      - Check network connectivity to Cloudera cluster
      - Ensure Hive Metastore is running and accessible
      - **For Non-Kerberos:** Verify HDFS user has appropriate permissions
      - **For Kerberos:**
         - Verify Kerberos principal is correct
         - Check keytab file is valid and not expired
         - Ensure `krb5.conf` has correct KDC information
         - Verify network connectivity to KDC
         - Check Hive Metastore supports Kerberos authentication
   13. Select **Apache Hive** as Catalog Type.
   14. Provide a **Catalog Name** (e.g., `sparkcatalog` for non-Kerberos or `<<catalog>>` for Kerberos).

      While creating component, the only available option under Associated catalog is Apache Hive.
      {: note}

   15. Click **Create** or **Save** button.
   16. Wait for component creation to complete (may take longer for Kerberos setup).
   17. Verify component appears in Infrastructure Manager list with Active status.

3. Associate catalog with Presto engine

   1. In Infrastructure Manager, go to **Engines** section.
   2. Select your Presto engine.
   3. Click **Associate Catalogs** or **Manage Catalogs**.
   4. Find your catalog in the available catalogs list.
   5. Click **Add** or toggle the switch to enable.
   6. Wait for the association to complete.
   7. Verify catalog appears in the engine's catalog list.

      Engine restart may be required for Kerberos configuration to take effect.
      {: note}

4. Verify catalog activation

   1. Go to **Query Workspace** in {{site.data.keyword.lakehouse_short}}.
   2. Run the following query:

      ```sql
      SHOW CATALOGS;
      ```
      {: codeblock}

      Expected output should include your catalog name along with system and other catalogs.

## Results
{: #data_stream_cloudera_presto_setup4}

The setup enables direct, zero-copy querying of Hive tables from Cloudera HDFS in {{site.data.keyword.lakehouse_short}}, eliminating the need for data replication. Both Kerberos and non-Kerberos authentication methods are supported.

After completing the setup, you can query your Cloudera tables. For information about querying operations, see [Querying Cloudera tables using Presto engine](/docs/watsonxdata?topic=watsonxdata-data_stream_cloudera_presto_query).

## Related information
{: #data_stream_cloudera_presto_setup5}

- [Integrating Cloudera in {{site.data.keyword.lakehouse_short}}](/docs/watsonxdata?topic=watsonxdata-data_stream_cloudera1)
- [Querying Cloudera tables using Presto engine](/docs/watsonxdata?topic=watsonxdata-data_stream_cloudera_presto_query)
- [Cloudera Data Platform documentation](https://docs.cloudera.com/)
- [Apache Hive documentation](https://hive.apache.org/)
- [Apache HDFS documentation](https://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/HdfsUserGuide.html)
