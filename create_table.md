---

copyright:
  years: 2022, 2023
lastupdated: "2023-11-29"

keywords: watsonxdata, data manager, create table

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

# Creating table
{: #create_table}

You can generate, configure, and run DDL from the **Data manager** page by using the web console.
{: shortdesc}

1. Log in to {{site.data.keyword.lakehouse_full}} console.
1. From the navigation menu, select **Data manager**.
1. Select the engine from the **Engine** menu. Catalogs that are associated with the selected engine are listed.
1. Click **Create table from file** and select **Create table from file**.
1. In the **Creating table from a file** form, drag a file to the box or click to upload.

   .CSV, .Parquet, .json, .txt are the supported data file formats.
   For .json file, you must enclose the content in `[]`.
   For .json file, multilevel data is not supported.
   {: note}

1. Click the data type and choose the required data types for each column. Click **Next**.
1. In the **Target** form, select the **Catalog**, and **Schema** in which the table is created.
1. Enter a name for the table in the **Table name** field, select **Table format**, **Date format**, and click **Next**. Do not use special character such as question mark (?) or asterisk (*) in table or column name.
1. Verify the details in the **Summary** page and scroll down to view the **DDL preview**.
1. Click **Create**.
1. Verify that the table creation status in the **Result set** is successful, indicated as true.
1. Go to the **Data manager** page and select the schema under which you created the table and click the refresh icon. The newly created table is listed.

Following are the requirements or limitations when ingesting data through web console:
* Iceberg target table is the only supported format.
* Partitioning is not supported.
* Source CSV file containing TAB or space as delimiter is not supported.
* Configure options are disabled for GA.
* Target table output format is Iceberg and the target data format is Parquet.
* Target storage path is default and cannot be changed.
