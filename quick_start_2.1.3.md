---

copyright:
  years: 2022, 2025
lastupdated: "2025-06-26"

keywords: lakehouse, watsonx data, quick start, engine, catalog, bucket
subcollection: watsonxdata

content-type: tutorial
services:
account-plan: paid
completion-time: 20m

---

{{site.data.keyword.attribute-definition-list}}

# Quick start {{site.data.keyword.lakehouse_short}} console
{: #quick_start_213}
{: toc-content-type="tutorial"}
{: toc-services=""}
{: toc-completion-time="20m"}

When you log in to the {{site.data.keyword.lakehouse_full}} web console for the first time, you are presented with the quick start wizard. In this tutorial, you learn how to use the quick start wizard to configure the core components and get started with {{site.data.keyword.lakehouse_short}} in a few minutes.
{: shortdesc}

The wizard guides you through the initial configuration process for the infrastructure components of {{site.data.keyword.lakehouse_short}}.

## Configure a storage
{: #qs_bucket_213}
{: step}

Your {{site.data.keyword.lakehouse_short}} needs an object storage bucket to store your raw data files. You can provision a new IBM-managed bucket or register your own bucket. You can add more buckets and register them later. You can also configure the query monitoring details. You can enable or disable the query monitoring to store and manage your diagonostic data.

In the **Configure storage** section, complete the following steps:

1. Select one of the following options and provide details.
   - **Discover COS instance** : Selects an existing IBM COS instance and an attached bucket on your IBM Cloud account. If multiple IBM COS instances and buckets are detected, select the IBM COS instance that contains the desired bucket to register with {{site.data.keyword.lakehouse_short}}.
   - **Register my own** :  You can use any existing IBM COS bucket from an existing instance or provision a new instance. To provision a new IBM COS instance, provide the following details:

     | Field | Description |
     |--------------------------|----------------|
     | Bucket Type | Select from Amazon S3, IBM Storage Ceph, or IBM Cloud Object Storage.|
     |Region | The region where the data bucket is available.|
     | Bucket Name | Enter your bucket name.|
     | Display name | Enter the bucket name to be displayed on-screen.|
     | Endpoint | Enter the endpoint URL.|
     | Access key | Enter your access key. |
     | Secret key | Enter your secret key. |
     | Connection status | Click the **Test connection** link to test whether the bucket connection with {{site.data.keyword.lakehouse_short}} is successful or not. The system displays the status message.|
     {: caption="Add bucket " caption-side="bottom"}


   If you select an existing IBM COS bucket, the default size is 10 GB. It is meant for an exploratory purpose and cannot be used to store production or sensitive data. The {{site.data.keyword.lakehouse_short}} instance administrators can disable this bucket for compliance reasons.

   When you register your own bucket, ensure to provide the correct details for bucket configuration. The quick start wizard does not validate the bucket configuration details and you cannot modify them later.
   {: note}

In the **Query monitoring** section, complete the following steps:


1. Use the toggle switch to enable (or disable) the query monitoring feature, and the associated catalog that appears with the query monitoring bucket will be of type Hive.

2. If you enable the QHMM feature, you need to configure the storage details for storing QHMM data. Select one of the following options and provide details.

   - **Discover COS instance** : Selects an existing IBM COS instance and an attached bucket on your IBM Cloud account. If multiple IBM COS instances and buckets are detected, select the IBM COS instance that contains the desired bucket to register with {{site.data.keyword.lakehouse_short}}.
   - **Register my own** : You can register an existing bucket as a QHMM bucket. Only the following bucket types can be registered as a QHMM bucket: Amazon S3, IBM Storage Ceph, or IBM Cloud Object Storage. To register an existing bucket as QHMM bucket, provide the following details:

     | Field | Description |
     |--------------------------|----------------|
     | Bucket Type | Select from Amazon S3, IBM Storage Ceph, or IBM Cloud Object Storage.|
     |Region | The region where the data bucket is available.|
     | Bucket Name | Enter your bucket name.|
     | Display name | Enter the bucket name to be displayed on-screen.|
     | Endpoint | Enter the endpoint URL.|
     | Access key | Enter your access key. |
     | Secret key | Enter your secret key. |
     | Connection status | Click the **Test connection** link to test whether the bucket connection with {{site.data.keyword.lakehouse_short}} is successful or not. The system displays the status message.|
     {: caption="Add bucket " caption-side="bottom"}

   The storage (default or BYOB) can be changed at later point from the {{site.data.keyword.lakehouse_short}} console page. See [Query monitoring]({{site.data.keyword.ref-qhmm-link}}){: external}.
   {: important}

4. Click **Next**.



## Configure a catalog
{: #qs_catalogs_213}
{: step}

Your {{site.data.keyword.lakehouse_short}} needs metadata catalogs to manage your table schemas. Creating the support services for the metadata catalog adds 3 RUs/Hr to your instance run rate when you complete the quickstart process.

In the **Configure catalog** page, complete the following steps:

1. Select the table format for managing your data. Apache Hive and Apache Iceberg catalogs are available.

To enable [Query monitoring]({{site.data.keyword.ref-qhmm-link}}){: external} feature, you must select Apache Hive catalog.
{: attention}

2. Click **Next**.

## Configure an engine
{: #qs_engine}
{: step}

Your {{site.data.keyword.lakehouse_short}} needs a query engine to work with your data.

In the **Configure engine** page, complete the following steps:

1. Select the engine to run and process the data that you attached.

2. Select the size of the engine based on the requirements of your workload.

   | Size | Description |
   |--------------------------|----------------|
   | Starter/Lite (IBM) (2 RUs/hour) | Includes 1 coordinator node and 1 worker node. All nodes are **Starter**. |
   | Starter (AWS) (5.6 RUs/hour) | Includes 1 coordinator node and 1 worker node. All nodes are cache-optimized. |
   | Small (11.2 RUs/hour) | Includes 1 coordinator node and 3 worker nodes. All nodes are cache-optimized. |
   | Medium (19.6 RUs/hour) | Includes 1 coordinator node and 6 worker nodes. All nodes are cache-optimized. |
   | Large (36.4 RUs/hour) | Includes 1 coordinator node and 12 worker nodes. All nodes are cache-optimized. |
   {: caption="Engine size " caption-side="bottom"}

3. Click **Next**.



## Review the configuration details
{: #qs_summary_213}
{: step}

In the **Summary** page, complete the following steps:

1. Review the configurations before you finish setting up your {{site.data.keyword.lakehouse_short}}.

2. Click **Finish and go**.

When the setup is complete, the {{site.data.keyword.lakehouse_short}} home page appears. Resource Unit consumption begins soon after creating the support services by using the quick start wizard. You can view the run rate that is submitted for billing from the billing and usage tab. For more information, see [Billing and usage]({{site.data.keyword.ref-manage_bill-link}}){: external}.

## Next steps
{: #qs_next_steps_213}

You are all set to use the {{site.data.keyword.lakehouse_short}} or you can configure it further.
