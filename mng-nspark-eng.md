---

copyright:
  years: 2017, 2024
lastupdated: "2024-04-30"

keywords: watsonx.data, spark, analytics, provisioning
subcollection: watsonxdata

---

{{site.data.keyword.attribute-definition-list}}

# Managing native Spark engine
{: #manage_nsp}

Native Spark engine allows you to do the following functionalities:


*** View and edit Native Spark engine details**
: You can use the IBM® watsonx.data UI or API to view and edit the Native Spark details. For more information, see [View and edit Native Spark engine details](watsonxdata?topic=watsonxdata-view_edit).

*** Manage user access**
: You can manage user access and infrastructure access for a native Spark engine. For more information, see [Managing user access for Native Spark engine](watsonxdata?topic=watsonxdata-manage_access).

*** View and manage applications**
: You can monitor the status of the applications that are submitted in the IBM® watsonx.data instance. Log in to the watsonx.data cluster. Go to the Infrastructure manager page. For more information, see [View and manage applications](watsonxdata?topic=watsonxdata-mng_appltn).

*** Scaling native Spark engine**
: You can increase or decrease the compute capacity of the native Spark engine by scaling. For more information, see [Scaling native Spark engine](watsonxdata?topic=watsonxdata-scl_nsp).

*** Pause or resume native Spark engine**
: You can pause a Spark engine, which is in running state. Pausing an engine stops the Spark applications in running state and the engine releases the existing capacity. You can also resume a paused engine. To pause an engine, see [Pausing native Spark engine](watsonxdata?topic=watsonxdata-pause_engine). To resume an engine, see [Resuming native Spark engine](watsonxdata?topic=watsonxdata-resume_engine).

Pause the native Spark engine when not in use to avoid accumulating additional charges. You can resume the engine later. It takes about 15-20 minutes to resume the engine.
{: note }

*** Associate or dissociate a catalog**
: You can associate (or dissociate an already associated catalog) a catalog with the Native Spark engine. To associate a catalog with the native Spark engine, see [Associating a catalog with an engine](watsonxdata?topic=watsonxdata-asso-cat-eng). To dissociate a catalog from the native Spark engine, see [Dissociating a catalog from an engine](watsonxdata?topic=watsonxdata-disso-cat-eng).

When you associate a catalog with a Spark engine, connection properties for the associated catalog are added to the Spark engine's default configuration. Do not overwrite these properties in default configuration manually.
 {: note}

*** Spark user interface**
: The Spark user interface (Spark UI) helps you to keep track of various aspects of a running Spark application. For more information, see [View and manage applications](watsonxdata?topic=watsonxdata-wxd_spk_ui).

*** Accessing the Spark history server**
: The Spark history server is a web UI where you can view the status of running and completed Spark applications on a watsonx.datainstance. For more information, see [Accessing the Spark history server](watsonxdata?topic=watsonxdata-wxd_spk_histry).
