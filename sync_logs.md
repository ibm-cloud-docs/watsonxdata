---

copyright:
  years: 2022, 2024
lastupdated: "2025-02-25"

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

# Syncing external data into {{site.data.keyword.lakehouse_short}}
{: #sync_log}

There may be different data objects on the external object store (bucket) than on the watsonx.data storage catalog. You can sync the object store (bucket) metadata of the storage with that of watsonx.data storage without moving the data manually. Syncing the metadata allows you to fetch the up-to-date data from the external buckets and select the respective watsonx.data catalog with the remote bucket. The respective catalog is to be attached to the storage for this feature.
{: shortdesc}


1. In the **Infrastructure Manager** page, click **Add component**.
2. Select the storage from the **Storage** section.
3. Enter the storage details.
3. Select **Activate now**.
4. Based on the type of table format, select one of the following **Catalog type**.

   - **Apache Iceberg**
   - **Apache Hive**
   - **Apache Hudi**
   - **Delta Lake**

   To register the tables, you must provide the exact location of the metatdata folder. The schema is inferred based on the path in the location url. Iceberg, Hive, Hui, and Delta Lake are the table formats supported.
   {: note}

5. Enter the catalog name.
6. Click **Create** to create the storage.
7. If you change the data in the storage bucket in {{site.data.keyword.lakehouse_short}} and you want to pull those changes then, go to the **Infrastructure manager** page, hover over the respective catalog and click Sync metadata. You can see three options to select the Mode and the corresponding possibility for metadata loss.
8. The following are the three sync options:
* **Register new objects only**: Schemas, tables, and metadata that are created by external applications since the last sync operations are added to this catalog. Existing schemas and tables in this catalog are not modified.
* **Update existing objects only**: Schemas, tables, and metadata already present in this catalog are updated or deleted to match the current state found in the associated bucket. Any other schemas, tables, and metadata in the associated bucket are ignored.
* **Sync all objects**: Schemas, tables, and metadata already present in this catalog are updated to match the exact state of the associated bucket. All the new objects are added and all the existing objects are updated or removed.

## Related API
{: #iceberg_api}

For information on related API, see
* [External Iceberg table registration](https://cloud.ibm.com/apidocs/watsonxdata-software#update-sync-catalog)
