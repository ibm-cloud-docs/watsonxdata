---

copyright:
  years: 2017, 2024
lastupdated: "2024-07-03"

keywords: watsonx.data, spark, analytics, provisioning
subcollection: watsonxdata

---

{{site.data.keyword.attribute-definition-list}}

# Debug the Spark application
{: #log_nsp}

The Engine home(bucket that you passed during Spark engine provisioning) enables you to monitor and debug the Spark application. Engine home contains logs and spark events for all the Spark applications submitted on the engine.

The following procedure details the steps to view logs of a Spark application.


1. Log in to your IBM Cloud account, navigate to the engine home bucket from the Cloud object store instance.
2. Go to the root path of the storage bucket. Navigate to the path spark/`<spark-engine-id>`/logs to review logs of the Spark applications submitted. Here, `<spark-engine-id>` is the id of the engine on which the application is executed.
3. For each application submitted on the Spark engine, a sub-path is created with the application ID to store the Spark application's driver and executor log files.
4. To review logs, download the driver and executors log file from the Cloud object storage console.
