---

copyright:
  years: 2022, 2025
lastupdated: "2025-08-26"

keywords: lakehouse, database, credentials, watsonx.data

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

# Updating data source or storage credentials
{: #up-db-cred}

To update the data source or storage credentials, use one of the following methods:
{: shortdesc}

- **Updating the data source and storage credentials in list view**

1. In **Data sources** or **Storage** tab, click the overflow menu and then click **Update credentials**.
2. In the **Update credentials** window, enter your data source or storage **Access key** and **Secret key**.
3. Click **Test connection** to validate and then click **Update**.

- **Updating the data source credentials in topology view**

1. Hover over the data source or storage for which you want to update the credentials.
2. Click the **Update credentials** icon.
3. In the **Update credentials** window, enter your data source or storage **Access key** and **Secret key**.
4. Click **Test connection** to validate and then click **Update**.

## Behaviour
{: #behaviour_cred}

For IBM managed buckets, there is no option to update credentials.
{: note}

* Presto:
   * **Update Credentials** is enabled for all external storage buckets and data sources, regardless of their association status with the engine.
   * When you update the credentials for a data source or storage linked to the Presto (C++) engine, the system applies the changes dynamically and automatically restarts the engine.
   * When you update the credentials for a data source or storage associated to the Presto (Java) engine, the changes are applied dynamically without a restart.

* Spark: **Update Credentials** is enabled for the storage buckets that has been designated as the Spark engine's home bucket during the provisioning process and all other external storage buckets and data sources, regardless of their association status with the engine. Spark synchronizes with the latest updated credentials of associated storages within 5-6 minutes.

* Milvus: **Update Credentials** is enabled for the home storage bucket associated with the Milvus service, and is followed by an automatic engine restart after the credentials are saved.

## Related API
{: #updatedb_api}

For information on related API, see
* [Update data source](https://cloud.ibm.com/apidocs/watsonxdata#update-database)
