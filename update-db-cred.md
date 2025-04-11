---

copyright:
  years: 2022, 2025
lastupdated: "2025-04-11"

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

Presto: **Update credentials** is disabled for storage buckets and data sources when associated with Presto. To update the credentials, you will need to disassociate the storage buckets and data sources, update the credentials and then associate it.

Spark: Though the **Update credentials** is enabled, updating the access credentials for a storage bucket and data sources that has been designated as the Spark engine's home bucket during the provisioning process can lead to data access problems and operational failures.

Milvus: For external home bucket and data sources, **Update credentials** is enabled, but a manual pause and resume of the Milvus engine is required for the changes to take effect.

   For IBM managed bucket and data sources, there is no option to update credentials.



## Related API
{: #updatedb_api}

For information on related API, see
* [Update data source](https://cloud.ibm.com/apidocs/watsonxdata#update-database)
