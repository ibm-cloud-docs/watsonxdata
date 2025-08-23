---

copyright:
  years: 2017, 2025
lastupdated: "2025-08-23"

keywords: watsonx.data, spark, analytics, provisioning
subcollection: watsonxdata

---

{{site.data.keyword.attribute-definition-list}}

# Managing native Spark engine
{: #manage_nsp}

**Applies to** : [Spark engine]{: tag-blue}  [Gluten accelerated Spark engine]{: tag-green}

Native Spark engine allows you to do the following functionalities:


**View and edit Native Spark engine details**
: You can use the IBM® watsonx.data UI or API to view and edit the Native Spark details. For more information, see [View and edit Native Spark engine details]({{site.data.keyword.ref-view_edit-link}}).

**Manage user access**
: You can manage user access and infrastructure access for a native Spark engine. For more information, see [Managing user access for Native Spark engine]({{site.data.keyword.ref-manage_access-link}}).

**View and manage applications**
: You can monitor the status of the applications that are submitted in the IBM® watsonx.data instance. Log in to the watsonx.data cluster. Go to the Infrastructure manager page. For more information, see [View and manage applications]({{site.data.keyword.ref-mng_appltn-link}}).

**Scaling native Spark engine**
: You can increase or decrease the compute capacity of the native Spark engine by scaling. For more information, see [Scaling native Spark engine]({{site.data.keyword.ref-scl_nsp-link}}).

**Pause or resume native Spark engine**
: You can pause a Spark engine, which is in running state. Pausing an engine stops the Spark applications in running state and the engine releases the existing capacity. You can also resume a paused engine. To pause an engine, see [Pausing native Spark engine]({{site.data.keyword.ref-pause_engine-link}}). To resume an engine, see [Resuming native Spark engine]({{site.data.keyword.ref-resume_engine-link}}).

Pause the native Spark engine when not in use to avoid accumulating additional charges. You can resume the engine later.
{: note }

**Associate or dissociate a catalog**
: You can associate (or dissociate an already associated catalog) a catalog with the Native Spark engine. To associate a catalog with the native Spark engine, see [Associating a catalog with an engine]({{site.data.keyword.ref-asso-cat-eng-link}}). To dissociate a catalog from the native Spark engine, see [Dissociating a catalog from an engine]({{site.data.keyword.dissociate-catalog-link}}).

When you associate a catalog with a Spark engine, connection properties for the associated catalog are added to the Spark engine's default configuration. Do not overwrite these properties in default configuration manually.
 {: note}

**Spark user interface**
: The Spark user interface (Spark UI) helps you to keep track of various aspects of a running Spark application. For more information, see [View and manage applications]({{site.data.keyword.ref-wxd_spk_ui-link}}).

**Accessing the Spark history server**
: The Spark history server is a web UI where you can view the status of running and completed Spark applications on a watsonx.datainstance. For more information, see [Accessing the Spark history server]({{site.data.keyword.ref-wxd_spk_histry-link}}).
