---

copyright:
  years: 2024
lastupdated: "2025-05-15"
keywords: spark, interface
subcollection: watsonxdata

---

{{site.data.keyword.attribute-definition-list}}

[Spark]{: tag-spark}

[Gluten accelerated Spark]{: tag-GlutenacceleratedSpark}

[Data store]{: tag-datastore}

# Spark user interface
{: #wxd_spk_ui}

The Spark user interface (Spark UI) helps you to keep track of various aspects of a running Spark application.

The following list includes a few examples:

* current running stage
* number of tasks in a stage
* reason for a longer running stage
* strangler task in a stage
* whether the executors in the application are used optimally
* inspect into memory and disk consumption of the driver and executors


Use the Spark history server to inspect the run of a completed Spark application. To access the Spark history server, see the [Access Spark history server]({{site.data.keyword.ref-wxd_spk_histry-link}}).
{: note}

## Accessing the Spark UI
{: #wxd_spk_ui_acs}


1. Log in to {{site.data.keyword.lakehouse_short}} console.
2. From the navigation menu, select **Infrastructure manager**.
1. Click the name of the Spark engine (from list view or topology view). Engine information window opens.
2. In the **Applications** tab, select an application and click the application **ID** link. The **Spark UI** opens.
3. You can view the following details :

    * The **Event Time line** displays a graphical view of the timeline and the events.
    * Different stages of execution, the storage used, the Spark environment and executor (memory and driver) details.

Log links under the Stages and Executors tabs of the Spark history server UI will not work as logs are not preserved with the Spark events. To review the task and executor logs, enable platform logging. For details, see [Viewing logs](/docs/watsonxdata?topic=watsonxdata-log_nsp).
{: note}
