---

copyright:
  years: 2022, 2025
lastupdated: "2025-11-06"

keywords: lakehouse, MDS, {{site.data.keyword.lakehouse_short}}, hive, metastore

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

# Manually syncing Query Optimizer with {{site.data.keyword.lakehouse_short}} metastore
{: #sync_optimizer_meta}

## About this task
{: #optimizer_abtsync}

To provide optimized queries, **Query Optimizer** pulls data about table definitions and Hive and Iceberg statistics to synchronize with MDS in {{site.data.keyword.lakehouse_full}}. You can select the specific Hive and Iceberg table that must be available for **Query Optimizer**. It is recommended to generate Hive and Iceberg statistics and label columns for primary and foreign keys to get the best results.

Activating **Query Optimizer** automatically synchronizes metadata for catalogs that are connected to Presto (C++) engines. However, you will need to run the following steps if:

* Metadata for inaccessible or corrupted catalogs or schemas during deployment are missing.
* Significant changes are made to a table.
* New tables are introduced after the initial sync operation.
* An intermittent issue is preventing tables from being synced during the automatic syncing process upon activation.

## Before you begin
{: #optimizer_bybsync}

To sync tables from {{site.data.keyword.lakehouse_short}}, the following items are required:

   The instructions in this topic can now be executed using the enhanced feature [Managing statistical updates from the Optimizer dashboard](/docs/watsonxdata?topic=watsonxdata-analyze_optimizer), which enables advanced query performance enhancements and optimization capabilities across multiple
   catalogs.
   {: note}

1. Verify that all expected tables are synced by following the procedure in [Verifying table sync in watsonx.data](/docs/watsonxdata?topic=watsonxdata-sync_optimizer_verify).

1. Identify the list of Hive and Iceberg tables in {{site.data.keyword.lakehouse_short}} that you require for **Query Optimizer**.

1. Identify columns as primary and foreign keys in the Hive and Iceberg tables.

1. `ANALYZE` Hive and Iceberg tables in Presto (C++) to generate Hive and Iceberg statistics.

1. Only users with administrator privilege is allowed to run `ExecuteWxdQueryOptimizer` command as a security enhancement feature.

1. If the session parameter `is_query_rewriter_plugin_enabled` is set to `false`, you will not be able to execute the `ExecuteWxdQueryOptimizer` commands.

## Procedure
{: #optimizer_prosync}

1. Log in to {{site.data.keyword.lakehouse_short}}.
2. Go to **Query workspace**.
3. Run the `ANALYZE` command from the {{site.data.keyword.lakehouse_short}} web console for the tables that you want to sync to generate the statistics (Statistics is the number of rows, column name, data_size, row count, and more).

   ```bash
   ANALYZE catalog_name.schema_name.table_name ;
   ```
   {: codeblock}

4. Run the following command to manually register the metastore properties of catalog in the **Query Optimizer** {{ site.data.keyword.undata_short }} the legacy metastore type `watsonx-data` for both Hive and Iceberg catalogs:

   ```bash
   ExecuteWxdQueryOptimizer 'CALL SYSHADOOP.REGISTER_EXT_METASTORE('<CATALOG_NAME>', '<ARGUMENTS>', ?, ?)';
   ```
   {: codeblock}

   ```bash
   ExecuteWxdQueryOptimizer 'CALL SYSHADOOP.REGISTER_EXT_METASTORE('<CATALOG_NAME>','type=watsonx-data,uri=thrift://<THRIFT_URL>,use.SSL=true,authmode=PLAIN,ssl.cert=/secrets/external/ibm-lh-tls-secret/ca.crt,auth.plain.credentials=<USERNAME>:<PASSWORD>', ?, ?)
   ```
   {: codeblock}

   For example:
   ```bash
   ExecuteWxdQueryOptimizer 'CALL SYSHADOOP.REGISTER_EXT_METASTORE('iceberg_data','type=watsonx-data,uri=thrift://ibm-lh-lakehouse-mds-thrift-svc.zen.svccluster.local:8380,use.SSL=true,auth.mode=PLAIN,ssl.cert=/secrets/external/ibm-lh-tls-secret/ca.crt,auth.plain.credentials=admin:password', ?, ?)';
   ```
   {: codeblock}

   - `type` - The type of metastore to which you are connecting. Supported value is: `watsonx-data`.
   - `watsonx.data <CATALOG_NAME>` - as shown on the Infrastructure Manager page (case sensitive).
   - `<THRIFT_URL>` - As obtained from the Infrastructure Manager page (click on the catalog).
   - MDS credentials (`<Username>` and `<Password>`) in `auth.plain.credentials` - Must be created on the watsonx.data side. See Connecting to watsonx.dataon OpenShift. If the metastore requires PLAIN authentication, the credentials must be specified in the format `username:password` or `ibmlhapikey_<username>:apikey`. The password is stored securely in a software keystore.
   - `auth.mode` - If the metastore requires authentication, indicates the mode of authentication to use. The auth.mode must be set to PLAIN
   - `use.SSL` - It must be true if the metastore requires an SSL connection.
   - `<MDS certificate file path>` - This must be provided as a file on the db2u container as a certificate to validate the SSL connection. It is notnecessary to pass a certificate if the SSL connection is established using a certificate issued by a well known CA such as DigiCert or VeriSign. Bydefault, the MDS certificates are available under the `/secrets/external/ibm-lh-tls-secret/ca.crt` path in Query optimizer.
      1. Run the following command to identify the db2u Query Optimizer head pod (OPT_POD).

         ```bash
         oc get pod | grep oaas-db2u
         ```
         {: codeblock}

      2. Run the following command to generate certificate by substituting the values for `<OPT_POD>` and `<Metastore Thrift endpoint>`.

         ```bash
         oc exec -it <OPT_POD> -c db2u -- bash -c "echo QUIT | openssl s_client -showcerts -connect <Metastore Thrift endpoint> | awk '/-----BEGIN   CERTIFICATE-----/           {p=1}; p; /-----END CERTIFICATE-----/ {p=0}' > /tmp/mds.pem"
         ```
         {: codeblock}



4. Run the following command to register {{site.data.keyword.lakehouse_short}} catalog with **Query Optimizer**:

   ```bash
   ExecuteWxdQueryOptimizer 'CALL SYSHADOOP.REGISTER_EXT_METASTORE('<CATALOG_NAME>','type=watsonx-data,uri=thrift://<Metastore_Thrift_endpoint>,use.SSL=true,auth.mode=PLAIN,auth.plain.credentials=<Username>:<apikey>', ?, ?)';
   ```
   {: codeblock}

   * `<CATALOG_NAME>` - as shown on the Infrastructure Manager page (case-sensitive).
   * `<Metastore_Thrift_endpoint>` - As obtained from the Infrastructure Manager page (Click the catalog).
   * MDS Credentials (`<Username>`:`<apikey>`) - Must be created on the {{site.data.keyword.lakehouse_short}}. See [Connecting to watsonx.data on IBM Cloud or Amazon Web Services](https://www.ibm.com/docs/en/db2woc?topic=integration-connecting-watsonxdata-cloud-amazon-web-services).

   Registering the catalog with the **Query Optimizer** allows watsonx.data tables to be synced into the **Query Optimizer**, enabling query optimization. This needs to be run one time for each catalog.
   {: note}

5. Run the following command to synchronize the tables for each schema in the catalog:

   ```bash
   ExecuteWxdQueryOptimizer 'CALL SYSHADOOP.EXT_METASTORE_SYNC('<CATALOG_NAME>', '<SCHEMA_NAME>', '.*', '<SYNC MODE>', 'CONTINUE', 'OAAS')';
   ```
   {: codeblock}

   * `<CATALOG_NAME>`: The name of the catalog where the tables to synchronize belong to.
   * `<SCHEMA_NAME>`: The name of the schema where the tables to synchronize belong to.
   * `<SYNC MODE>`: `SKIP` is a sync mode indicating the objects that are already defined should be skipped. `REPLACE` is another sync mode used to update the object if it has been modified since last synched.
   * `CONTINUE`: The error is logged, but processing continues if multiple tables are to be imported.

   When synchrnization is completed, the output displays the list of synced tables. The total count of synced tables must be double the number of tables within the catalog or schema. This is because, each table are synced two times. Once from the external metastore to the local metastore, and then from the local metastore to the Db2 catalog.
   {: note}

   Verify the sync operation in a few minutes by following the procedure in [Verifying table sync in watsonx.data](/docs/watsonxdata?topic=watsonxdata-sync_optimizer_verify).
   {: note}

6. Identify the list of catalogs and schemas in watsonx.data that you require for **Query Optimizer**.

   Provide an SQL file to define the constraints for the **Query Optimizer** to use. In the SQL file, identify primary keys, foreign keys, and not null columns where applicable for each table in your data set.

   For example, if you have the following three tables with the given columns,

   Employees (EmployeeID, FirstName, LastName, Department, and Salary), Departments (DepartmentID and DepartmentName), and EmployeeDepartmentMapping (MappingID, EmployeeID, and DepartmentI).

   Run the `ALTER` table command to define the constraints:

   ```bash
   -- NOT NULL
   ExecuteWxdQueryOptimizer 'ALTER TABLE "catalog_name".schema_name.Employees ALTER COLUMN FirstName SET NOT NULL ALTER COLUMN LasttName SET NOT NULL ALTER COLUMN Salary SET NOT NULL ALTER COLUMN EmployeeID SET NOT NULL';
   ExecuteWxdQueryOptimizer 'ALTER TABLE "catalog_name".schema_name.Departments ALTER COLUMN DepartmentName SET NOT NULL ALTER COLUMN DepartmentID SET NOT NULL ';
   ExecuteWxdQueryOptimizer 'ALTER TABLE "catalog_name".schema_name.EmployeeDepartmentMapping ALTER COLUMN MappingID SET NOT NULL ';
   -- PRIMARY KEY
   ExecuteWxdQueryOptimizer 'ALTER TABLE "catalog_name".schema_name.Employees ADD PRIMARY KEY (EmployeeID) NOT ENFORCED';
   ExecuteWxdQueryOptimizer 'ALTER TABLE "catalog_name".schema_name.Departments ADD PRIMARY KEY (DepartmentID) NOT ENFORCED';
   ExecuteWxdQueryOptimizer 'ALTER TABLE "catalog_name".schema_name.EmployeeDepartmentMapping ADD PRIMARY KEY (MappingID) NOT ENFORCED';
   -- FOREIGN KEY
   ExecuteWxdQueryOptimizer 'ALTER TABLE "catalog_name".schema_name.EmployeeDepartmentMapping ADD FOREIGN KEY (EmployeeID) REFERENCES "catalog_name".schema_name.Employees(EmployeeID) NOT ENFORCED';
   ExecuteWxdQueryOptimizer 'ALTER TABLE "catalog_name".schema_name.EmployeeDepartmentMapping ADD FOREIGN KEY (DepartmentID) REFERENCES "catalog_name".schema_name.Departments(DepartmentID) NOT ENFORCED';
   ```
   {: codeblock}
