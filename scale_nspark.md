---

copyright:
  years: 2017, 2024
lastupdated: "2024-05-31"

keywords: watsonx.data, spark, analytics, provisioning
subcollection: watsonxdata

---

{{site.data.keyword.attribute-definition-list}}

# Scaling native Spark engine
{: #scl_nsp}

You can increase or decrease the compute capacity of the native Spark engine by scaling. Scale up your native Spark engine, if the Spark workloads require additional compute capacity and scale down if you need to release surplus compute capacity.

Scaling up the Spark engine results in additional charges. Ensure to scale down the unused storage capacity.
{: important}

To scale engine, use one of the following methods:
* Scaling an engine in list view
* Scaling an engine in topology view

## Scaling an engine in list view
{: #scl_1}

   1. Click the overflow menu icon at the end of the row and click **Scale**.
   2. In **Scale engine** window, enter the number of worker nodes in the **Worker nodes** field. To scale up, increase the worker node and to scale down, reduce the worker nodes.
   3. Click **Scale**.

## Scaling an engine in topology view
{: #scl_2}

   1. Hover over the engine that you want to scale and click the **Scale** icon.
   2. In **Scale engine** window, enter the number of worker nodes in the **Worker nodes** field. To scale up, increase the worker node and to scale down, reduce the worker nodes.
   3. Click **Scale**.
