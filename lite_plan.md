---

copyright:
  years: 2022, 2024
lastupdated: "2024-09-24"

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

When the allocated Resource Units or time runs out, the instance becomes inactive and you can no longer access it.
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

## Viewing usage
{: #hp_monitor_usg_lite}
{: step}

You can monitor the Resource Units usage level.

1. For the Lite plan, in the {{site.data.keyword.lakehouse_short}} UI, **Billing** section, you can view a widget that displays the Resource Unit consumption.

    You can also view the Resource Unit consumption from the **{{site.data.keyword.lakehouse_short}} console** UI > **Welcome** page > **Current plan** tile.
    {: note}

1. If the allocated Resource Units or time runs out, your Lite instance will be suspended. However, you can still launch the IBM Cloud instance , cannot use it. You can manually delete your IBM Cloud Lite instance by following the steps:

    1. Log in to your IBM Cloud account.
    2. Click **Resource list**. The list of resources appears.
    3. In **Resource list**, expand **Databases**.
    4. To delete an instance, click the overflow menu icon at the end of the row and click **Delete**. A delete confirmation dialog is displayed.
    5. Click **Delete**.

    For more information to manually delete an instance, see [Deleting instance](https://cloud.ibm.com/docs/watsonxdata?topic=watsonxdata-delete_lh).


## Getting started with {{site.data.keyword.lakehouse_short}}
{: #hp_start}
{: step}

The Lite plan usage consumption starts after you provision the instance. The resource units (RU) are consumed even when the {{site.data.keyword.lakehouse_short}} instance is not being used. However, RU consumption reduces if you pause or delete the engine. Therefore, pause the engines and services when not in use, to maximize the IBM Cloud Lite plan availability.
{: attention}


To simplify the steps, when you log in to the {{site.data.keyword.lakehouse_short}} web console for the first time, you are directly presented with the **Welcome to {{site.data.keyword.lakehouse_short}}** landing page and the UI includes components (engines, services and storages) based on the use case selected.

For more information about the different use cases, see [watsonx.data Lite plan](watsonxdata?topic=watsonxdata-tutorial_prov_lite_1).

To begin with, {{site.data.keyword.lakehouse_short}} UI provides on-sctreen instructions that guide you through the steps to run a Presto query using sample worksheet and perform data ingestion.

### Querying data using sample worksheet and performing ingestion
{: #hp_start-step}

1. From the [**Resource list**](https://cloud.ibm.com/resources) page, under the **Databases** category, you can see that the status for your instance as, **Provision in progress**. Click the {{site.data.keyword.lakehouse_short}} instance link when the status changes to **Active**.


2. From the **Welcome to {{site.data.keyword.lakehouse_short}}** page, you can select one of the following options :
    **Take a homepage tour** : to view a guided home page tour to learn more about the entry points in the home page.
    **Start working with data** : to run sample query using the sample worksheets and to try ingetsing data in watsonx.data.

    You can also skip this step (use the **Skip for now** link) and go to the Welcome page directly and explore the UI features.
    {: note}

3. If you select the **Start working with data** option and click **Continue**, you can view the following tiles:
    **Explore a sample worksheet** : {{site.data.keyword.lakehouse_short}} Lite plan instance provides sample worksheets (includes query) that help users to run Presto query easily. Select this tile and follow the on-screen instructions to run your first Presto query.
    **Ingest data into watsonx.data** : Select this tile to perform data ingestion.

4. If you select **Explore a sample worksheet**, the **Query workspace** page opens and the **Sample worksheets** section is highlighted.

5. Select the worksheet and click **Run on Prestoplus**. The query is executed successfully and you can view the query result in the **Results** section..

    You can also explore more **Query workspace** related functionalities. See, [Running SQL queries](watsonxdata?topic=watsonxdata-run_sql).

6. If you select **Ingest data into watsonx.data**, the **Data manager** page opens.

7. Before you begin to ingest data, configure the storage for ingestion.

8. Click **Set up now**. The **Finish set up** page opens.

    a. With no existing IBM COS instance:

      * If user does not have an existing IBM COS instance, a new IBM COS instance is provisioned with default name and a new bucket is attached to it with standard name (wxd-inst id).

      * Click **Finish**.

      * In the IBM COS account, the new IBM COS instance and the new bucket exists.

    b. With existing IBM COS instance:


      If the user has COS instance in a trial account, it is fetched and a new bucket with standard name is attached to it.


9. Go to the **Infrastructure manager** and verify that the storage is associated with the engine and the Spark engine is in running status, without which you cannot perform ingestion.

10. After you verify, go to the the **Data manager** page and click **Ingest data**. You can perform data ingestion. For more information, see [About data ingestion](watsonxdata?topic=watsonxdata-load_ingest_data).

You cannot scale the existing engine or service or add a new engine (or service). To add a new engine or service, you must delete the existing engine or service.

You can add only one Presto (Java) engine, Spark engine (single node, small size - 8 vCPU, 32GB node) and Milvus service (Milvus with size specification, Starter - 1 Million vectors, Index Parameters - 64, Segment size (1024)). To understand the restrictions, see [Lite plan features and restrictions](watsonxdata?topic=watsonxdata-pricing-plans-1).
{: important}

## Adding your own storage and querying data
{: #hp_ingest}
{: step}

You can add your own storage and ingest data into it.

1. From **Add Component** > **Storage** > **IBM COS storage** :

    For Lite plan instance, there are two options:

    a. **Discover COS instance** : Select the existing IBM COS instance and the bucket to be attached to it.

    b. **Register my own** : Provision a new IBM COS instance. See [Adding a storage-catalog pair](watsonxdata?topic=watsonxdata-reg_bucket#cos). You must provision and register new instance.


To explore how the {{site.data.keyword.lakehouse_short}} service interacts with the data you bring in, see [Adding your storage and querying data](watsonxdata?topic=watsonxdata-tutorial_prov_custbckt1).


## Saving data from a lite plan to an enterprise plan
{: #post_expry}
{: step}

When the allocated Resource Units or time expires, the instance becomes inactive and you can no longer access it.

If you choose to continue using watsonx.data by creating an Enterprise {{site.data.keyword.lakehouse_short}} instance, you can save the data from your lite plan to the enterprise plan. To do that, you need an IBM Cloud Object Store (COS) bucket to connect to your lite plan instance of watsonx.data. You can then write data to that COS bucket you own. Then, create an enterprise instance of watsonx.data, connect it to the same COS bucket that you own to keep working with the same data files.


1. Create a COS bucket to store data from the Lite plan. For more information, see [Create buckets to store data](https://cloud.ibm.com/docs/cloud-object-storage?topic=cloud-object-storage-getting-started-cloud-object-storage#gs-create-buckets).

1. Ingest data from Lite plan instance to the COS bucket. For more information, see [Adding the storage that you own and ingesting data](watsonxdata?topic=watsonxdata-tutorial_prov_custbckt1#hp_ingest1).

2. Either before or after your lite plan has concluded, create an enterprise plan instance. For more information, see [Enterprise plan](watsonxdata?topic=watsonxdata-getting-started_1).

3. Go to the **Quick start watsonx.data console** > **Configure bucket** page, specify the COS bucket details that you own (which stores data from the Lite plan). For more information, see [Quick start {{site.data.keyword.lakehouse_short}} console](watsonxdata?topic=watsonxdata-quick_start).

When the setup is complete, the watsonx.data home page (enterprise plan) opens. From the navigation menu, select **Data manager** to view the COS storage bucket with data from the lite plan.
