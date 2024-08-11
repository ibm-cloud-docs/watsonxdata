---

copyright:
  years: 2022, 2024
lastupdated: "2024-08-11"

keywords: lakehouse, hms, {{site.data.keyword.lakehouse_short}}, hive, metastore

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

## Before you begin
{: #optimizer_bybsync}

To sync tables from {{site.data.keyword.lakehouse_full}}, the following items are required:

1. Identify the list of Hive tables in {{site.data.keyword.lakehouse_short}} that you require for **Query Optimizer**.

1. Identify columns as primary and foreign keys in the Hive tables.

1. `ANALYZE` Hive tables in Presto (C++) to generate Hive statistics.

## About this task
{: #optimizer_abtsync}

To provide optimized queries, **Query Optimizer** pulls data about table definitions and hive statistics to synchronize with Hive metastore in {{site.data.keyword.lakehouse_short}}. You can select the specific Hive table that must be available for **Query Optimizer**. It is recommended to generate Hive statistics and label columns for primary and foreign keys to get the best results.

Enabling **Query Optimizer** automatically synchronizes metadata for catalogs that are connected to Presto (C++) engines. However, you will need to run the following steps if:
* Metadata for inaccessible or corrupted catalogs or schemas during deployment are missing.
* Significant changes are made to a table.
* New tables are introduced after the initial sync operation.
* An intermittent issue is preventing tables from being synced during the automatic syncing process upon activation.

## Procedure
{: #optimizer_prosync}

1. Log in to {{site.data.keyword.lakehouse_short}}.
2. Go to **Query workspace**.
3. Run the `ANALYZE` command from the {{site.data.keyword.lakehouse_short}} web console for the tables that you want to sync to generate the statistics (Statistics is the number of rows, column name, data_size, row count, and more).

   ```bash
   ANALYZE catalog_name.schema_name.table_name ;
   ```
   {: codeblock}

4. Run the following command to register {{site.data.keyword.lakehouse_short}} catalog with **Query Optimizer**:

   ```bash
   ExecuteWxdQueryOptimizer "CALL SYSHADOOP.REGISTER_EXT_METASTORE('<CATALOG_NAME>','type=watsonx-data,uri=thrift://$LOCAL_HMS_URL,use.SSL=true,auth.mode=PLAIN,auth.plain.credentials=ibmlhapikey:<apikey>', ?, ?);
   ```
   {: codeblock}

   * Catalog name - as shown on the Infrastructure Manager page (case-sensitive).
   * HMS thrift uri - As obtained from the Infrastructure Manager page (Click the catalog).
   * HMS Credentials - Must be created on the {{site.data.keyword.lakehouse_short}}. See [Connecting to watsonx.data on IBM Cloud or Amazon Web Services](https://www.ibm.com/docs/en/db2woc?topic=integration-connecting-watsonxdata-cloud-amazon-web-services).

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
