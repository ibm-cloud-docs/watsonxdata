---

copyright:
  years: 2022, 2025
lastupdated: "2025-10-24"

keywords: lakehouse, storage, catalog, watsonx.data

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

# IBM Cloud Object Storage
{: #cos_storage}

IBM Cloud® Object Storage stores encrypted and dispersed data across multiple geographic locations.
{: shortdesc}

If you select **IBM Cloud Object Storage** from the **Storage** section, configure the following details:

 | Field | Description |
 |--------------------------|----------------|
 | Display name | Enter the name to be displayed. (The following special characters are not allowed: ! @ # $ % ^ & * ( ) = + : { } < > ? ' \ ; `).|
 | Bucket name | Enter the name of your existing bucket. If you do not have an existing bucket then you can create a new bucket. For more information, see [Create bucket](https://cloud.ibm.com/docs/cloud-object-storage?topic=cloud-object-storage-getting-started-cloud-object-storage#gs-create-buckets).|
 | Region | Select the region where the storage is available.|
 | Endpoint | Enter the Endpoint URL. Test connection is enabled when the endpoint is provided. \n Fetch the Endpoint by the following steps: \n 1. Go to IBM Cloud Console. \n 2. Select the service as IBM Cloud Object storage> Select your bucket. \n 3. Go to the Configuration tab> Click Endpoints. \n 4. Copy the Public endpoint address. \n * Create the Endpoint by the following steps: \n * Endpoints are created when bucket is configured. For more information, see [Configure Endpoint](https://cloud.ibm.com/docs/cloud-object-storage?topic=cloud-object-storage-endpoints).|
 | Access key | Enter your Access key. \n Fetch the credentials for access key by the following steps: \n 1. From the Resource list page, select the name of the service to open the service details page. \n 2. Click Service credentials. \n 3. Expand the row for the required access key credential. For more information, see [Viewing a credential](https://cloud.ibm.com/docs/account?topic=account-service_credentials&interface=ui#viewing-credentials-ui). \n * Create the credentials for access key by the following steps if you do not have it: \n 1. Create credentials for bucket. For more information, see [Service credentials](https://cloud.ibm.com/docs/cloud-object-storage?topic=cloud-object-storage-service-credentials). \n 2. Enable the HMAC toggle switch to get the Access Key and Secret Key paired for use with S3-compatible tools. For more information, see [Using HMAC credentials](https://cloud.ibm.com/docs/cloud-object-storage?topic=cloud-object-storage-uhc-hmac-credentials-main). |
 | Secret key | Enter your Secret key. \n Fetch the credentials for secret key by the following steps: \n 1. From the Resource list page, select the name of the service to open the service details page. \n 2. Click Service credentials. \n 3. Expand the row for the required secret key credential. For more information, see [Viewing a credential](https://cloud.ibm.com/docs/account?topic=account-service_credentials&interface=ui#viewing-credentials-ui). \n * Create the credentials for secret key by the following steps if you do not have it: \n 1. Create credentials for bucket. For more information, see [Service credentials](https://cloud.ibm.com/docs/cloud-object-storage?topic=cloud-object-storage-service-credentials). \n 2. Enable the HMAC toggle switch to get the Access Key and Secret Key paired for use with S3-compatible tools. For more information, see [Using HMAC credentials](https://cloud.ibm.com/docs/cloud-object-storage?topic=cloud-object-storage-uhc-hmac-credentials-main). |
 | Connection Status | Click the Test connection link to test the storage connection. If the connection is successful, a success message appears.|
| Designate this bucket as the ACL store | Use the toggle switch to designate this bucket as the ACL store. If you enable the toggle switch, \n An **Enable Access Control List (ACL)?** dialog appears, Click **Enable**. \n This feature applies to {{site.data.keyword.lakehouse_short}} Premium, for more information see [Governance through Access Controlled Lists (AC)](https://dataplatform.cloud.ibm.com/docs/content/wsj/wx-data/gov_acl.html?context=wxd&audience=wdp). If you enable the toggle switch, the Associate catalog option is selected by default, with the Apache Iceberg catalog preselected. You cannot choose a different catalog for ACLs. You can designate only one storage as the ACL store per instance. After a storage is designated, this option will no longer be visible. |
 | Associate Catalog | Enable the toggle switch to add a catalog for your storage. This catalog is associated with your storage and serves as your query interface with the data stored within. |
 | Catalog type | Select the catalog type from the list. The recommended catalog is Apache Iceberg. The other options for catalog are Apache Hive, Apache Hudi, and Delta Lake.|
 | Catalog name | Enter the name of your catalog. (The following special characters are not allowed: ! @ # $ % ^ & * ( ) = + : { } < > ? ' \ ; `).|
 | Associate | Click Associate to create the storage. |
 {: caption="Register bucket" caption-side="bottom"}

If IBM Cloud Object Storgae is already inactive in old instances, the system will display the `Activate` button. Once you activate IBM Cloud Object Storgae, the system will automatically remove the `Activate` button.
{: note}
