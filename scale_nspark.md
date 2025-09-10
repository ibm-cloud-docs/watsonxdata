---

copyright:
  years: 2022, 2025
lastupdated: "2025-09-10"

keywords: watsonx.data, spark, analytics, provisioning
subcollection: watsonxdata

---

{{site.data.keyword.attribute-definition-list}}

# Scaling native Spark engine
{: #scl_nsp}


**Applies to** : [Spark engine]{: tag-blue}  [Gluten accelerated Spark engine]{: tag-green}


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

## Scaling Spark engine by using API
{: #scl_nsp_api}

**Sample V2 API**

```bash
curl -X POST -H "content-type: application/json" -H "AuthInstanceId: {CRN}" "https://{region}.lakehouse.cloud.ibm.com/lakehouse/api/v2/spark_engines/{engine_id}/scale"-d '{  "number_of_nodes": 2}'

```
{: codeblock}

Parameter values:

   {CRN} : The **Instance CRN** of your watsonx.data instance. To retrieve the CRN, see [Getting connection information]({{site.data.keyword.ref-get_connection-link}}).
   {id} : Engine id of Spark engine when using REST API based `SPARK` ingestion.
   {instance id} : Enter the instance ID. You can get the instance ID from the {{site.data.keyword.lakehouse_short}} instance home page (information icon). |


**Sample V3 API**

```bash
curl -X POST -H "content-type: application/json" -H "AuthInstanceId: {instance id}" "https://{region}.lakehouse.cloud.ibm.com/lakehouse/api/v3/spark_engines/{id}/scale"-d '{  "number_of_nodes": 2}'

```
{: codeblock}

Parameter values:

   {CRN} : The **Instance CRN** of your watsonx.data instance. To retrieve the CRN, see [Getting connection information]({{site.data.keyword.ref-get_connection-link}}).
   {id} : Engine id of Spark engine when using REST API based `SPARK` ingestion.
   {instance id} : Enter the instance ID. You can get the instance ID from the {{site.data.keyword.lakehouse_short}} instance home page (information icon). |
