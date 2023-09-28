---

copyright:
  years: 2022, 2023
lastupdated: "2023-09-27"

keywords: lakehouse, bucket, catalog, watsonx.data

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

# Adding a bucket-catalog pair
{: #reg_bucket}

A bucket is an existing, externally managed object storage. It is one of the data sources for {{site.data.keyword.lakehouse_full}}. A catalog defines the schemas and metadata for a data source.
{: shortdesc}

When you add your own object storage bucket or database, or query the data in these data sources through the query engines of {{site.data.keyword.lakehouse_short}}, egress charges for pulling data out of these sources might apply depending on your service provider. If you are using managed services, consult your service provider's documentation or support for details about these charges.
{: important}

To reduce the latency issues, it is recommended to colocate your additional object storage buckets or databases in the region where {{site.data.keyword.lakehouse_short}} instance is provisioned.
{: important}


To add a bucket-catalog pair, complete the following steps.

1. Log in to the {{site.data.keyword.lakehouse_short}} console.
2. From the navigation menu, select **Infrastructure Manager**.
3. To define and connect a bucket, click **Add component** and select **Add bucket**.
4. In the **Add bucket** window, provide the following details to connect to existing externally managed object storage.

   | Field | Description |
   |--------------------------|----------------|
   | Bucket type | Select the bucket type from the list.|
   | Bucket name | Enter your existing object storage bucket name.|
   | Display name | Enter the name to be displayed.|
   | Endpoint | Enter the endpoint URL.|
   | Access key | Enter your access key. |
   | Secret key | Enter your secret key. |
   | Activation| Activate the bucket immediately or activate it later. |
   | Catalog type | Select the catalog type from the list.|
   | Catalog name | Enter the name of your catalog. This catalog is automatically associated with your bucket.|
   {: caption="Table 1. Register bucket" caption-side="bottom"}

5. Click **Add**.
