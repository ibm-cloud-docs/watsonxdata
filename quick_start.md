---

copyright:
  years: 2022, 2024
lastupdated: "2024-02-28"

keywords: lakehouse, watsonx data, quick start, engine, catalog, bucket
subcollection: watsonxdata

content-type: tutorial
services:
account-plan: paid
completion-time: 20m

---

{{site.data.keyword.attribute-definition-list}}

# Quick start {{site.data.keyword.lakehouse_short}} console
{: #quick_start}
{: toc-content-type="tutorial"}
{: toc-services=""}
{: toc-completion-time="20m"}

When you log in to the {{site.data.keyword.lakehouse_full}} web console for the first time, you are presented with the quick start wizard. In this tutorial, you learn how to use the quick start wizard to configure the core components and get started with {{site.data.keyword.lakehouse_short}} in a few minutes.
{: shortdesc}

The wizard guides you through the initial configuration process for the infrastructure components of {{site.data.keyword.lakehouse_short}}.

## Configure a bucket
{: #qs_bucket}
{: step}

Your {{site.data.keyword.lakehouse_short}} needs an object storage bucket to store your raw data files. You can provision a new IBM-managed bucket or register your own bucket. You can add more buckets and register them later.

In the **Configure bucket** page, complete the following steps:

1. Select one of the following options and provide details.
   - Provision new IBM-managed bucket
   - Register my own

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
     {: caption="Table 1. Add bucket " caption-side="bottom"}

2. Click **Next**.

The IBM-managed bucket is a default 10 GB bucket. It is meant for an exploratory purpose and cannot be used to store production or sensitive data. The {{site.data.keyword.lakehouse_short}} instance administrators can disable this bucket for compliance reasons.

When you register your own bucket, ensure to provide the correct details for bucket configuration. The quick start wizard does not validate the bucket configuration details and you cannot modify them later.
{: note}

## Configure a catalog
{: #qs_catalogs}
{: step}

Your {{site.data.keyword.lakehouse_short}} needs metadata catalogs to manage your table schemas. Creating the support services for the metadata catalog adds 3 RUs/Hr to your instance run rate when you complete the quickstart process.

In the **Configure catalog** page, complete the following steps:

1. Select the table format for managing your data. Apache Hive and Apache Iceberg catalogs are selected by default.

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
   | Starter (IBM) (2 RUs/hour) | Includes 1 coordinator node and 1 worker node. All nodes are **Starter**. |
   | Starter (AWS) (5.6 RUs/hour) | Includes 1 coordinator node and 1 worker node. All nodes are cache-optimized. |
   | Small (11.2 RUs/hour) | Includes 1 coordinator node and 3 worker nodes. All nodes are cache-optimized. |
   | Medium (19.6 RUs/hour) | Includes 1 coordinator node and 6 worker nodes. All nodes are cache-optimized. |
   | Large (36.4 RUs/hour) | Includes 1 coordinator node and 12 worker nodes. All nodes are cache-optimized. |
   {: caption="Table 2. Engine size " caption-side="bottom"}

3. Click **Next**.

## Review the configuration details
{: #qs_summary}
{: step}

In the **Summary** page, complete the following steps:

1. Review the configurations before you finish setting up your {{site.data.keyword.lakehouse_short}}.

2. Click **Finish and go**.

When the setup is complete, the {{site.data.keyword.lakehouse_short}} home page appears. Resource Unit consumption begins soon after creating the support services by using the quick start wizard. You can view the run rate that is submitted for billing from the billing and usage tab. For more information, see [Billing and usage](watsonxdata?topic=watsonxdata-manage_bill){: external}

## Next steps
{: #qs_next_steps}

You are all set to use the {{site.data.keyword.lakehouse_short}} or you can configure it further.
