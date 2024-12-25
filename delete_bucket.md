---

copyright:
  years: 2022, 2024
lastupdated: "2024-12-25"

keywords: lakehouse, bucket, watsonx.data

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

# Deleting a storage-catalog pair
{: #delete_bucket}

To delete a storage-catalog pair, complete the following steps:
{: shortdesc}


1. Dissociate the catalog that is associated with the storage from the engine. For instructions, see [Dissociating a catalog from an engine]({{site.data.keyword.dissociate-catalog-link}}){: external}.

2. In **Infrastructure manager**, go to the **Storage** tab.

3. Click the overflow menu and then click **Deactivate**.

4. In the **Confirm deactivation** window, click **Deactivate**.

5. Click the overflow menu and then click **Delete**.

6. In the **Confirm removal** window, click **Delete**.

## Related API
{: #deletebck_api}

For information on related API, see
* [Deregister bucket](https://cloud.ibm.com/apidocs/watsonxdata#delete-bucket-registration)
* [Activate bucket](https://cloud.ibm.com/apidocs/watsonxdata#create-activate-bucket)
* [Deactivate bucket](https://cloud.ibm.com/apidocs/watsonxdata#delete-deactivate-bucket)
