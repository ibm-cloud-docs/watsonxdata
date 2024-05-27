---

copyright:
  years: 2017, 2024
lastupdated: "2024-04-30"

keywords: watsonx.data, spark, analytics, provisioning
subcollection: watsonxdata

---

{{site.data.keyword.attribute-definition-list}}

# Provisioning Native Spark engine
{: #prov_nspark}

{{site.data.keyword.lakehouse_full}} allows you to provision Native Spark engine to run complex analytical workloads.

## Before you begin
{: #prereq_nspark_prov}


1. Create a new Cloud Object Storage and a bucket. For more information, see [Creating a storage bucket][def]. This storage is considered as Engine home, which stores the Spark events and logs that are generated while running spark applications.
1. Register the Cloud Object Storage bucket. For more information, see [Adding a storage-catalog pair](watsonxdata?topic=watsonxdata-reg_bucket).

## Procedure
{: #pros_nspark_prov}

1. Log in to the {{site.data.keyword.lakehouse_short}} console and go to **Infrastructure manager**.
1. Click **Add component** and select **Add engine**.
1. In the **Add engine** window, provide the following details:

   | Field | Description |
   | --- | --- |
   | Type | Select **Spark** engine from the list. |
   | Display name | Enter your compute engine name. |
   | Default Spark version | Select **Spark runtime version** that must be considered for processing the applications. |
   | System bucket | Select the registered Cloud Object Storage bucket from the list to stores the Spark events and logs that are generated while running spark applications. \n Make sure you do not select the IBM-managed bucket as Spark Engine home. If you select IBM-managed bucket, you cannot access it to view the logs.{: note} |
   {: caption="Table 1. Provisioning Spark engine" caption-side="bottom"}

1. Reserve compute capacity for the Spark engine.
   1. Select the **Node Type**.
   1. Enter the number of nodes in the **No of nodes** field.
1. Click **Provision**. An acknowledgment message is displayed.

   Provisioning time of the native Spark engine varies depending on the number and type of nodes you add to the engine.
   {: note}


[def]: https://cloud.ibm.com/docs/cloud-object-storage?topic=cloud-object-storage-secure-content-store#create-cos-bucket
