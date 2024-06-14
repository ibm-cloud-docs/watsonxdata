---

copyright:
  years: 2022, 2024
lastupdated: "2024-05-31"

keywords: lakehouse, ingesting data, create table

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

# Creating table from a file
{: #import_data}

Files can also be ingested or imported to {{site.data.keyword.lakehouse_full}} through the overflow menu of schema in the **Data explorer** page to create tables.
{: shortdesc}

1. Log in to the {{site.data.keyword.lakehouse_short}} console.

1. From the navigation menu, select **Data manager**.

1. Select the engine from the **Engine** drop-down. Catalogs that are associated with the selected engine are listed.

1. There are two ways to import a file to create table. Select the required option:

    * Option 1: To import file to any available schema under a catalog, do the following steps:

        a. Click **Create** drop-down.

        b. Click **Create table from file**. The **Create table from a file** page opens.

        c. Go to step 5.

    * Option 2: To import file to a particular schema under the catalog, do the following steps:

        a. Select a schema under a catalog where you want to import a file to create table.

        b. Click the overflow menu of the selected schema and select **Create table from a file**. The **Create table from a file** page opens.

1. In the **Creating table from a file** form, drag a file to the box or click to upload.

   CSV, .Parquet, .JSON, .TXT are the supported data file formats.
   Creating a table from a file is only supported by iceberg catalogs.
   For JSON file, you must enclose the content in `[]`.
   The default file format for Hive is ORC and for Iceberg is Parquet.
   {: note}

   You can apply the configuration for Encoding, Escape character, Field delimiter, and Line delimiter prior to uploading any .CSV and .TXT files. Default values are as follows:
   Encoding value: UTF-8
   Escape character: \\
   Field delimiter: ,
   Line delimiter: \n
   {: note}

1. Click the data type and choose the required data types for each column. Click **Next**.
1. In the **Target** form, select the **Catalog**, and **Schema** in which the table is created.
1. Enter a name for the table in the **Table name** field, select **Table format**, **Date format**, and click **Next**. Do not use special character such as question mark (?) or asterisk (*) in table or column name.
1. Verify the details in the **Summary** page and scroll down to view the **DDL preview**.
1. Click **Create**.
1. Verify that the table creation status in the **Result set** is successful, indicated as true.
1. Go to the **Data manager** page and select the schema under which you created the table and click the refresh icon. The newly created table is listed.








