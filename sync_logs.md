---

copyright:
  years: 2022, 2024
lastupdated: "2024-11-30"

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

# Syncing external Iceberg data into {{site.data.keyword.lakehouse_short}}
{: #sync_log}

You can write data to object store by using any engine and other external tools in Iceberg table format that is outside {{site.data.keyword.lakehouse_short}}. You can sync the object store (bucket) metadata of the storage with {{site.data.keyword.lakehouse_short}} without moving the data physically. The Apache Iceberg catalog is to be attached to the storage for this feature.
{: shortdesc}


1. In the **Infrastructure Manager** page, click **Add component**.
2. Select the storage from the **Storage** section.
3. Enter the storage details.
3. Select **Activate now**.
4. Select **Catalog type** as **Apache Iceberg**.
5. Enter the catalog name.
6. Click **Create** to create the storage.
7. If you change the data in the storage bucket in {{site.data.keyword.lakehouse_short}} and you want to pull those changes then, go to the **Infrastructure manager** page, hover over the Apache Iceberg catalog and click Sync metadata. You can see three options to select the Mode and the corresponding possibility for metadata loss.
8. The following are the three sync options:
* **Register new objects only**: Schemas, tables, and metadata that are created by external applications since the last sync operations are added to this catalog. Existing schemas and tables in this catalog are not modified.
* **Update existing objects only**: Schemas, tables, and metadata already present in this catalog are updated or deleted to match the current state found in the associated bucket. Any other schemas, tables, and metadata in the associated bucket are ignored.
* **Sync all objects**: Schemas, tables, and metadata already present in this catalog are updated to match the exact state of the associated bucket. All the new objects are added and all the existing objects are updated or removed.

## Related API
{: #iceberg_api}

For information on related API, see [External Iceberg table registration](https://cloud.ibm.com/apidocs/watsonxdata-software#update-sync-catalog).
