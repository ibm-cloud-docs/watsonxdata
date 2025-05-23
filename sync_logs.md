---

copyright:
  years: 2022, 2025
lastupdated: "2025-04-24"

keywords: lakehouse, database, tags, description, watsonx.data

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

# Registering external data into {{site.data.keyword.lakehouse_short}}
{: #sync_log}

If you have pre-existing data (such as Iceberg, Delta, or Hudi tables) in an object store bucket, you can register it into {{site.data.keyword.lakehouse_full}} and use it for running queries. To enable this feature, you must attach the appropriate catalog to the storage.

You can register tables in all three formats. For Iceberg tables, you can register pre-existing data at the bucket level. For Delta and Hudi tables, registration is currently supported only at the table level.

If external changes occur on Iceberg tables through other systems, you may need to sync the data on the {{site.data.keyword.lakehouse_short}} side. To facilitate this, you can use sync feature.

For Hudi and Delta tables, explicit sync is unnecessary because the metadata pointer refers to the metadata folder, not an individual metadata file. (For example, Iceberg requires referencing the latest metadata.json file.)

## Registering and syncing external Iceberg data
{: #extrnl_ice}

To register and sync external Iceberg data into watsonx.data, complete the following steps:

1. Add a storage and associate it to the **Apache Iceberg** catalog, see [Adding storage](/docs/watsonxdata?topic=watsonxdata-reg_bucket).
2. To pull the changed data in a storage bucket in {{site.data.keyword.lakehouse_short}}, go to the **Infrastructure manager** page, hover over the Apache Iceberg catalog and click Sync metadata. You can see three options to select the Mode and the corresponding possibility for metadata loss. The following are the three sync options:

* **Register new objects only**: Schemas, tables, and metadata that are created by external applications since the last sync operations are added to this catalog. Existing schemas and tables in this catalog are not modified.
* **Update existing objects only**: Schemas, tables, and metadata already present in this catalog are updated or deleted to match the current state found in the associated bucket. Any other schemas, tables, and metadata in the associated bucket are ignored.
* **Sync all objects**: Schemas, tables, and metadata already present in this catalog are updated to match the exact state of the associated bucket. All the new objects are added and all the existing objects are updated or removed.

For information on related API, see [External Iceberg table registration](https://cloud.ibm.com/apidocs/watsonxdata-software#update-sync-catalog).

## Registering external Hudi and Delta Lake data
{: #extrnl_hudi_delta}

To register external Hudi and Delta Lake data into watsonx.data, complete the following steps:

1. Add a storage and based on the type of table format, you can select one of the following **Catalog type**. See [Adding storage](/docs/watsonxdata?topic=watsonxdata-reg_bucket).

   - **Apache Hudi**
   - **Delta Lake**
2. You can register and load table using [Register table](https://cloud.ibm.com/apidocs/watsonxdata-software#register-table) and [load table metadata](https://cloud.ibm.com/apidocs/watsonxdata-software#load-table) APIs.

   To register the tables, you must provide the exact location of the metatdata folder. The schema is inferred based on the path in the location url.
   {: #note}
