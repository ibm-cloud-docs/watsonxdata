---

copyright:
  years: 2017, 2021
lastupdated: "2024-12-28"
keywords: watsonx.data, history, Spark, server

subcollection: watsonxdata

---


{{site.data.keyword.attribute-definition-list}}


{:step: data-tutorial-type="step"}
{:shortdesc: .shortdesc}


# Accessing the Spark history server
{: #wxd_spk_histry}

The Spark history server is a web UI where you can view the status of running and completed Spark applications on a {{site.data.keyword.lakehouse_short}}instance. If you want to analyze how different stages of your Spark application performed, you can view the details in the Spark history server UI.


1. Log in to {{site.data.keyword.lakehouse_short}} console.
2. From the navigation menu, select **Infrastructure manager**.
1. Click the name of the Spark engine (from list view or topology view). Engine information window opens.
2. In the **Spark history** tab, click **Start history server**.
3. By default, the Spark history server consumes 1 CPU core and 4 GiB of memory while it is running. If you want your Spark history server to use more resources, select the **Cores** and **Memory** required for the server and click **Start**. The history server starts and the status is displayed as `STARTED`.
3. Click **View Spark history**. The **History Server** page opens.
4. The **History Server** page includes the following functionalities:

    * View the list of completed Spark application and details such as the application ID, duration and event log for each application.
    * Click **Download** link from the **Event Log** field to download the events log information for each application.
    * To view the details of individual application, click the individual application ID link. The **Spark Jobs** page opens. This page displays details such as the different stages of execution, the storage used, the Spark environment and executor (memory and driver) details.

5. You can stop the history server when you no longer need it to release unnecessary resources. To do that, go to **Spark history** tab and click **Stop history server**. Click **Stop** on the confirmation message.

## Related API
{: #sparkhistoryui_api}

For information on related API, see
* [Get spark engine catalog](https://cloud.ibm.com/apidocs/watsonxdata#get-spark-engine-catalog)
* [Get spark history server](https://cloud.ibm.com/apidocs/watsonxdata#get-spark-engine-history-server)
* [Start spark history server](https://cloud.ibm.com/apidocs/watsonxdata#start-spark-engine-history-server)
* [Stop spark history server](https://cloud.ibm.com/apidocs/watsonxdata#delete-spark-engine-history-server)
