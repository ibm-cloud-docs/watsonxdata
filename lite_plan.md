---

copyright:
  years: 2022, 2024
lastupdated: "2024-09-25"

keywords: watsonx.data, lite, plan, instance

subcollection: watsonxdata

content-type: tutorial
account-plan: paid
completion-time: 10 minutes
---


{{site.data.keyword.attribute-definition-list}}


{:step: data-tutorial-type="step"}
{:shortdesc: .shortdesc}


# Working with the {{site.data.keyword.lakehouse_short}} Lite plan
{: #tutorial_hp_intro}
{: toc-content-type="tutorial"}
{: toc-completion-time="0.25h"}


The **Lite** plan allows you to provision an {{site.data.keyword.lakehouse_full}} instance that is free to use, with limits on capacity (2000 Resource Units), and features for a time frame of 30 days. You can use the account to create Lite plan instance based on three different use cases (Generative AI, High Performance BI and Data Engineering Workloads), explore and familiarize yourself with {{site.data.keyword.lakehouse_short}}. For more information about the features and limitations of Lite plan, see [Lite plan](watsonxdata?topic=watsonxdata-pricing-plans-1#limitations-lite){: external}.
{: shortdesc}

When the allocated Resource Units or time runs out, all Lite instances become inactive and you can no longer access it.
{: important}

To access all the features and functionalities without resource or time limit, you must have an [Enterprise {{site.data.keyword.lakehouse_short}} instance](watsonxdata?topic=watsonxdata-getting-started_1){: external} in a paid IBM Cloud account.

In this tutorial, you learn how to provision {{site.data.keyword.lakehouse_short}} instance (lite plan) and explore its features.



## Before you begin
{: #hp_byb}

To provision {{site.data.keyword.lakehouse_short}} Lite plan instance, you must have a trial account (or a paid account) on the IBM Cloud.
IBM Cloud trial accounts can have only one resource group. To create an IBM Cloud trial account, see [Trial account](https://cloud.ibm.com/docs/account?topic=account-accounts#trial).


## Provisioning {{site.data.keyword.lakehouse_short}} Lite plan
{: #hp_view_1}
{: step}

To provision a Lite plan instance, see [Provisioning {{site.data.keyword.lakehouse_short}} Lite plan](watsonxdata?topic=watsonxdata-tutorial_prov_lite_1).



## Getting started with {{site.data.keyword.lakehouse_short}} Lite plan UI
{: #hp_start}
{: step}

The Lite plan usage consumption starts after you provision the instance. The resource units (RU) are consumed even when the {{site.data.keyword.lakehouse_short}} instance is not being used. To monitor usage, see [Viewing usage](#hp_monitor_usg_lite). However, RU consumption reduces if you pause or delete the engine. Therefore, pause the engines and services when not in use, to maximize the IBM Cloud Lite plan availability. To pause an engine, see [Pausing an engine](watsonxdata?topic=watsonxdata-pause_engine) and to delete an engine, see [Deleting an engine](watsonxdata?topic=watsonxdata-delete_engine).
{: attention}

1. After you provision a Lite plan instance, you are directly presented with the **Welcome to {{site.data.keyword.lakehouse_short}}** window and the UI includes components (engines, services, and storages) based on the use case selected. You can also relaunch the console page. To do that see, [Open the web console](watsonxdata?topic=watsonxdata-tutorial_prov_lite_1#open_console-2).


## Selecting the guided workflow
{: #hp_02}
{: step}

To begin with the {{site.data.keyword.lakehouse_short}} features, UI provides on-screen instructions that take you through guided workflows to run a Presto query by using sample worksheet and perform data ingestion.


2. From the **Welcome to {{site.data.keyword.lakehouse_short}}** window, select one of the following options :

    * **Take a home page tour** : to view the home page tour to learn more about the entry points in the home page.

    * **Start working with data** : to run sample query by using the sample worksheets and to try ingesting data in watsonx.data.

    * **Skip for now** link : to view the watsonx.data home page without proceeding to the home tour or to work with watsonx.data.



## Querying data by using sample worksheet
{: #hp_03}
{: step}

Use the **Start working with data** option to query data.

3. If you select the **Start working with data** option and click **Continue**, you can view the following tiles:

    * **Explore a sample worksheet** : {{site.data.keyword.lakehouse_short}} Lite plan instance provides sample worksheets (includes query) that help users to run Presto query easily. Select this tile and follow the on-screen instructions to run your first Presto query.

    * **Ingest data into watsonx.data** : Select this tile to perform data ingestion.


4. If you select **Explore a sample worksheet**, the **Query workspace** page opens and the **Sample worksheets** section is highlighted.

5. Select the worksheet and click **Run on `<engine>`**. The query is executed successfully and you can view the query result in the **Results** section..

    You can also explore more **Query workspace** related functionalities. See, [Running SQL queries](watsonxdata?topic=watsonxdata-run_sql).

## Selecting storage and performing data ingestion
{: #hp_04}
{: step}

Use the **Ingest data into watsonx.data** option for data ingestion. Before performing data ingestion, associate a storage. If you use a trial account, a new IBM Cloud Object Storage instance is automatically provisioned with default name (watsonx-data-cos), and a new bucket is attached with default name (watsonx-data-instanceId). If you use a paid account, you must provision a new IBM Cloud Object Storage instance from [Create COS instance](https://cloud.ibm.com/objectstorage/create){: external} page.

6. If you select **Ingest data into watsonx.data**, the **Data manager** page opens.

7. Before you begin to ingest data, configure the storage for ingestion.

8. Click **Set up now**. The **Finish set up** page opens.


    a. If you use a trial account:

      * If the user does not have an IBM COS instance, a new IBM COS instance is provisioned with default name (watsonx-data-cos) and a new bucket is attached to it with default name (watsonx-data-instanceId). If the user has an IBM COS instance, a new bucket is attached to it with default name (watsonx-data-instanceId) to that instance.
      * Click **Finish**.


    b. If you use a Paygo account:


      * If the user has an IBM COS instance in a Paygo account, it is fetched and a new bucket with default name is attached to it.
      * If the user does not have an IBM COS instance, you must provision a new IBM COS instance. From the **Finish set up** page, click **Create new instance** to create a new COS instance. Select the storage.
      * Click **Finish**.


    You can also add storage from **Infrastructure manager** page and ingest data into it.

    1. From **Add Component** > **Storage** > Select the storage :

       To add the first bucket, some tiles for storages are disabled with the message: "Register a bucket from the available options first." Buckets to be added are enabled based on the available engines and services at that time. The buckets that meet the criteria for the available engines are enabled to be added as the first bucket.

       * For Spark: IBM COS storage, Amazon S3.
       * For Presto (Java): IBM COS storage, Amazon S3, Google Cloud Storage.
       * For Presto (C++): IBM COS storage, Amazon S3, Google Cloud Storage.
       * For Milvus: IBM COS storage, Amazon S3, MinIO, Azure Data Lake Storage, Google Cloud Storage.

    2. From **Add Component** > **Storage** > **IBM COS storage** :

        For Lite plan instance, there are two options:

        a. **Discover COS instance** : Select the existing IBM COS instance and the bucket to be attached to it.

        b. **Register my own** : Provision a new IBM COS instance. See [Create COS instance](https://cloud.ibm.com/objectstorage/create){: external}. You must provision and register new instance.


    To explore how the {{site.data.keyword.lakehouse_short}} service interacts with the data you bring in, see [Adding your storage and querying data](watsonxdata?topic=watsonxdata-tutorial_prov_custbckt1).

9. Go to the **Infrastructure manager** and verify that the storage is associated with the engine and the Spark engine is in running status, without which you cannot perform ingestion.

10. After you verify, go to the the **Data manager** page and click **Ingest data**. You can perform data ingestion. For more information, see [About data ingestion](watsonxdata?topic=watsonxdata-load_ingest_data).

You cannot scale the existing engine or service or add a new engine (or service). To add a new engine or service, you must delete the existing engine or service.

You can add only one Presto (Java) engine, Spark engine (single node, small size - 8 vCPU, 32GB node) and Milvus service (Milvus with size specification, Starter - 1 Million vectors, Index Parameters - 64, Segment size (1024)). To understand the restrictions, see [Lite plan features and restrictions](watsonxdata?topic=watsonxdata-pricing-plans-1).
{: important}



## Exploring the Query History Monitoring and Management
{: #qhm_func}
{: step}

The feature is disabled by default for Lite plan instance. To enable the feature, see [Enabling QHMM](watsonxdata?topic=watsonxdata-tutorial_prov_custbckt1)
and explore more, see [QHMM](watsonxdata?topic=watsonxdata-ovrvw_qhmm).


## Viewing usage
{: #hp_monitor_usg_lite}
{: step}

You can monitor the Lite plan Resource Units usage level from two places in the {{site.data.keyword.lakehouse_short}} console.

1. For the Lite plan, in the {{site.data.keyword.lakehouse_short}} UI, **Billing** section, you can view a widget that displays the Resource Unit consumption.

    You can also view the Resource Unit consumption from the **{{site.data.keyword.lakehouse_short}} console** UI > **Welcome** page > **Current plan** tile.
    {: note}

1. If the allocated Resource Units or time runs out, your Lite instance will be suspended. However, you can still launch the IBM Cloud instance, but cannot use it. You can manually delete your IBM Cloud Lite instance by following the steps:

    1. Log in to your IBM Cloud account.
    2. Click **Resource list**. The list of resources appears.
    3. In **Resource list**, expand **Databases**.
    4. To delete an instance, click the overflow menu icon at the end of the row and click **Delete**. A delete confirmation dialog is displayed.
    5. Click **Delete**.

    For more information to manually delete an instance, see [Deleting instance](https://cloud.ibm.com/docs/watsonxdata?topic=watsonxdata-delete_lh).


## Continuing to an enterprise plan
{: #post_expry}
{: step}

When the allocated Resource Units or time expires, the instance becomes inactive and you can no longer access it.

If you choose to continue using watsonx.data by creating an Enterprise {{site.data.keyword.lakehouse_short}} instance, you can use the same storage that has data from your Lite plan. 

2. Either before or after your lite plan has concluded, create an enterprise plan instance. For more information, see [Enterprise plan](watsonxdata?topic=watsonxdata-getting-started_1).

3. Go to the **Quick start watsonx.data console** > **Configure bucket** page, specify the COS bucket details that you own (which stores data from the Lite plan). For more information, see [Quick start {{site.data.keyword.lakehouse_short}} console](watsonxdata?topic=watsonxdata-quick_start).

When the setup is complete, the watsonx.data home page (enterprise plan) opens. From the navigation menu, select **Data manager** to view the COS storage bucket with data from the Lite plan.
