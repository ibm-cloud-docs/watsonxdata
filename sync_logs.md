---

copyright:
  years: 2022, 2024
lastupdated: "2024-04-03"

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

You can write data to object store by using Spark and other external tools like Snowflake in Iceberg table format that is outside {{site.data.keyword.lakehouse_short}}. You can sync the object store (bucket) metadata with {{site.data.keyword.lakehouse_short}} without moving the data physically.
{: shortdesc}


1. In Infrastructure Manager, click **Add component**.
2. Click **Add bucket**.
3. Enter the bucket details.
3. Select **Activate now**.
4. Select **Catalog type** as **Apache Iceberg**.
5. Enter the catalog name.
6. Select all the data present on the bucket to sync or create a catalog without any preexisting data.
7. After registration, click the catalog and go to **Sync logs**. You can see the status of synchronization (success, failure, partial success) and the last sync time.
8. After completing the synchronization, go to the **Data manager**. You can see the catalog that you created and the tables that are pulled from the bucket created by Snowflake.
9. If Snowflake user makes data changes in the bucket and watsonx.data wants to pull those changes in the bucket, then click **Sync data** from UI for three strategy options:
* **Sync all data**: Synchronize all the data or update the existing table that was promoted earlier.
* **Sync new data only**: Pull the newly created table only.
* **Sync existing data only**: Update the table registered earlier to the latest changes only.
