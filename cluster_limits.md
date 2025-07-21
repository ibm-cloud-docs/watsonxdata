---

copyright:
  years: 2017, 2022
lastupdated: "2025-07-21"

subcollection: watsonxdata

---

{{site.data.keyword.attribute-definition-list}}

# Default instance limits for engines and services
{: #wxd_clust_limits}

The following tables provide the default instance limits for engines and services. These default values are set to avoid excessive billing. However, you can contact IBM support to increase these limits.

The values listed here are global defaults for the Enterprise plan. Individual regions can have different default values. Also, you can request adjustments for your specific instances as required. For the Lite plan limitations, see [Lite plan limitations](/docs/watsonxdata?topic=watsonxdata-getting-started#limitations-lite).
{: note}

## Spark
{: #wxd_clust_limits_spark}

| Scenario | Default value | Error message if the limit exceeds |
| --- | --- | --- |
| The maximum number of Spark engines per {{site.data.keyword.lakehouse_short}} instance | 3 | The new engine or service cannot be created. You have reached the maximum limit of <*your engine limit*> engines or services. Delete other engines or services, or contact IBM support to request an increase to the limit. |
| The maximum number of compute nodes per Spark engine (provisioning) | 20 | Additional compute resources cannot be allocated to your instance because you have reached the maximum limit of <*your Spark node limit*> compute nodes. Scale down (or delete) other engines to free up more compute resources to be allocated to this engine. Contact IBM support to request an increase to the limit. |
| The maximum number of compute nodes per Spark engine (scaling) | 20 | Only <*available node count*> additional compute nodes can be allocated to your instance, as the current maximum limit is <*your Spark node limit*> compute nodes. Contact IBM support to request an increase to the limit. |
| The maximum number of Spark nodes per watsonx.data instances | 60 | Additional compute resources cannot be allocated to your instance because you have reached the maximum limit of <*your instance node limit*> compute nodes. Scale down (or delete) other engines to free up more compute resources to be allocated to this engine. Contact IBM support to request an increase to the limit. |
{: caption="Default instance limits for Spark" caption-side="bottom"}

## Presto
{: #wxd_clust_limits_presto}

| Scenario | Default value | Error message if the limit exceeds |
| --- | --- | --- |
| The maximum number of Presto engines per {{site.data.keyword.lakehouse_short}} instance | 2 | The new engine or service cannot be created. You have reached the maximum limit of <*your engine limit*> engines or services. Delete other engines or services, or contact IBM support to request an increase to the limit. |
| The maximum number of compute nodes per Presto engine (provisioning) | 10 | Additional compute resources cannot be allocated to your instance because you have reached the maximum limit of <*your Presto node limit*> compute nodes. Scale down (or delete) other engines to free up more compute resources to be allocated to this engine. Contact IBM support to request an increase to the limit. |
| The maximum number of compute nodes per Presto engine (scaling) | 10 | Only <*available node count*> additional compute nodes can be allocated to your instance, as the current maximum limit is <*your Presto node limit*> compute nodes. Contact IBM support to request an increase to the limit. |
{: caption="Default instance limits for Presto" caption-side="bottom"}

## Milvus
{: #wxd_clust_limits_milvus}

| Scenario | Default value | Error message if the limit exceeds |
| --- | --- | --- |
| The maximum number of Milvus services per {{site.data.keyword.lakehouse_short}} instance | 3 | The new engine or service cannot be created. You have reached the maximum limit of <*your engine limit*> engines or services. Delete other engines or services, or contact IBM support to request an increase to the limit. |
{: caption="Default instance limits for Milvus" caption-side="bottom"}
