---

copyright:
  years: 2022, 2024
lastupdated: "2025-02-24"

keywords: monitoring, watsonx.data

subcollection: watsonxdata

---

{{site.data.keyword.attribute-definition-list}}


# Monitoring for {{site.data.keyword.lakehouse_short}}
{: #monitor_wxd}

Provide insight about your {{site.data.keyword.lakehouse_full}} instance. View metrics on the health of key {{site.data.keyword.lakehouse_short}} components such as the metastore and engine. Also, understand the usage of your instances by actively running tasks and queries.
{: shortdesc}

You can use the IBM Cloud Monitoring service to monitor your {{site.data.keyword.lakehouse_short}} instance. {{site.data.keyword.lakehouse_short}} forwards selected information about your instance to Monitoring so that you can monitor specific metrics such as cpu and memory utilization.

## Before you begin
{: #setup_bb}

You must have view access to the **Sysdig** dashboard. For more information about providing the access, see [Getting started with IBM Cloud Monitoring](https://cloud.ibm.com/docs/monitoring?topic=monitoring-getting-started#getting-started).


## Set up your {{site.data.keyword.lakehouse_short}} service instance
{: #setup_wxd}

To set up Monitoring for {{site.data.keyword.lakehouse_short}}, you must create a service instance and then enable **Platform Metrics** in the same region as the {{site.data.keyword.lakehouse_short}} instance that you want to monitor. If you have deployments in more than one region, you must provision **Monitoring** and enable platform metrics for each region.



To set up {{site.data.keyword.mon_short}},

1. From the {{site.data.keyword.cloud_notm}} navigation menu, select **Observability**.
2. Select **Monitoring**. The **Monitoring** pane opens.
3. Either use an existing {{site.data.keyword.mon_short}} service instance or create a new one.
4. After the instance is ready, enable platform metrics by clicking **Configure platform metrics**.
5. Select a region and then a {{site.data.keyword.mon_short}} instance from that region. If you have deployments in more than one region, you must provision {{site.data.keyword.mon_short}} and enable platform metrics for each region.


## Accessing your {{site.data.keyword.mon_full_notm}} metrics
{: #access_monitor}


To see your {{site.data.keyword.lakehouse_full}} customer metrics dashboards in {{site.data.keyword.mon_short}}:

1. From the {{site.data.keyword.cloud_notm}} navigation menu, select **Observability**.

2. Select **Monitoring**. Click **Open Dashboard**.

3. Click **Dashboards** in the sidepane, open the **{{site.data.keyword.lakehouse_full}}** dashboard to view your {{site.data.keyword.lakehouse_short}} metrics.

4. For more information, see [{{site.data.keyword.mon_short}} Getting started tutorial](https://cloud.ibm.com/docs/monitoring?topic=monitoring-getting-started).
{: important}





## Metrics available by Service Plan
{: #metrics-by-plan}


* [MDS health status](#ibm_watsonx_data_hms_health)
* [Number of total running queries](#ibm_watsonx_data_queries_running_total)
* [Number of total running tasks](#ibm_watsonx_data_tasks_running_total)
* [Number of total transactions](#ibm_watsonx_data_transactions_total)
* [List of currently available catalogs](#ibm_watsonx_data_catalogs)
* [Presto health status](#ibm_watsonx_data_presto_health)
* [Total number of active nodes](#ibm_watsonx_data_active_nodes_total)
* [Total number of inactive nodes](#ibm_watsonx_data_inactive_nodes_total)
* [Total number of nodes](#ibm_watsonx_data_nodes_total)


### MDS health status
{: #ibm_watsonx_data_hms_health}


| Metadata | Description |
|----------|-------------|
| `Metric Name` | ibm_watsonx_data_mds_health|
| `Metric Type` | gauge |
| `Value Type`  | none |
| `Segment By` | Service Instance, Resource group |
| `Metric Description` | Checks the status of Postgres DB connection in MDS pod. |
{: caption="Table 2: MDS Health Status metric metadata" caption-side="top"}


### Number of total running queries
{: #ibm_watsonx_data_queries_running_total}


| Metadata | Description |
|----------|-------------|
| `Metric Name` | ibm_watsonx_data_queries_running_total|
| `Metric Type` | gauge |
| `Value Type`  | none |
| `Segment By` | Service Instance, Resource group |
| `Metric Description` | Runs Query to get the total queries that are in Running state in Presto Server. |
{: caption="Table 6: Number Of Total Running Queries metric metadata" caption-side="top"}

### Number of total running tasks
{: #ibm_watsonx_data_tasks_running_total}


| Metadata | Description |
|----------|-------------|
| `Metric Name` | ibm_watsonx_data_tasks_running_total|
| `Metric Type` | gauge |
| `Value Type`  | none |
| `Segment By` | Service Instance, Resource group |
| `Metric Description` | Shows the data that is collected by name-value pair collection for tasks in Presto server and populates the tables in the database. |
{: caption="Table 7: Number Of Total Running Tasks metric metadata" caption-side="top"}

### Number of total transactions
{: #ibm_watsonx_data_transactions_total}

| Metadata | Description |
|----------|-------------|
| `Metric Name` | ibm_watsonx_data_transactions_total|
| `Metric Type` | gauge |
| `Value Type`  | none |
| `Segment By` | Service Instance, Resource group |
| `Metric Description` | Shows the data that is collected by name-value pair collection for transactions in Presto server and populates the tables in the database. |
{: caption="Table 8: Number Of Total Transactions metric metadata" caption-side="top"}


### List of currently available catalogs
{: #ibm_watsonx_data_catalogs}


| Metadata | Description |
|----------|-------------|
| `Metric Name` | ibm_watsonx_data_catalogs|
| `Metric Type` | gauge |
| `Value Type`  | none |
| `Segment By` | Service Instance, Resource group |
{: caption="Table 3: List Of Currently Available Catalogs metric metadata" caption-side="top"}


### Presto health status
{: #ibm_watsonx_data_presto_health}


| Metadata | Description |
|----------|-------------|
| `Metric Name` | ibm_watsonx_data_presto_health|
| `Metric Type` | gauge |
| `Value Type`  | none |
| `Segment By` | Service Instance, Resource group |
| `Metric Description` | Tracks the heartbeat status by checking if the Presto server is running or not running. |
{: caption="Table 9: Presto Health Status metric metadata" caption-side="top"}

### Total number of active nodes
{: #ibm_watsonx_data_active_nodes_total}


| Metadata | Description |
|----------|-------------|
| `Metric Name` | ibm_watsonx_data_active_nodes_total|
| `Metric Type` | gauge |
| `Value Type`  | none |
| `Segment By` | Service Instance, Resource group |
| `Metric Description` | The total number of active nodes in the Presto Co-ordinator Pod. |
{: caption="Table 10: Total Number Of Active Nodes metric metadata" caption-side="top"}

### Total number of inactive nodes
{: #ibm_watsonx_data_inactive_nodes_total}


| Metadata | Description |
|----------|-------------|
| `Metric Name` | ibm_watsonx_data_inactive_nodes_total|
| `Metric Type` | gauge |
| `Value Type`  | none |
| `Segment By` | Service Instance, Resource group |
| `Metric Description` | The total number of inactive nodes in the Presto Co-ordinator Pod. |
{: caption="Table 11: Total Number Of Inactive Nodes metric metadata" caption-side="top"}

### Total number of nodes
{: #ibm_watsonx_data_nodes_total}


| Metadata | Description |
|----------|-------------|
| `Metric Name` | ibm_watsonx_data_nodes_total|
| `Metric Type` | gauge |
| `Value Type`  | none |
| `Segment By` | Service Instance, Resource group |
| `Metric Description` | The total number of nodes in the Presto Co-ordinator Pod. |
{: caption="Table 12: Total Number Of Nodes metric metadata" caption-side="top"}



## Attributes for segmentation
{: #attributes}

### Global attributes
{: #global-attributes}

The following attributes are available for segmenting all of the metrics that are listed above.

| Attribute | Attribute Name | Attribute Description |
|-----------|----------------|-----------------------|
| `Cloud Type` | `ibm_ctype` | The cloud type is a value of public, dedicated, or local |
| `Location` | `ibm_location` | The location of the monitored resource - this can be a region, data center or global |
| `Resource` | `ibm_resource` | The resource being measured by the service - typically an indentifying name or GUID |
| `Resource Type` | `ibm_resource_type` | The type of the resource being measured by the service |
| `Scope` | `ibm_scope` | The scope is the account, organization, or space GUID associated with this metric |
| `Service name` | `ibm_service_name` | Name of the service generating this metric |
{: caption="Table 13: Global attributes" caption-side="top"}

### Additional attributes
{: #additional-attributes}

The following attributes are available for segmenting one or more attributes as described in the reference above. See the individual metrics for segmentation options.

| Attribute | Attribute Name | Attribute Description |
|-----------|----------------|-----------------------|
|`Catalog in the Presto Server`|`ibm_watsonx_data_catalog`|Catalog in the Presto Server|
|`Catalog name`|`ibm_watsonx_data_catalog_name`|Catalog name|
|`Resource role`|`ibm_watsonx_data_resource_role`|Role in the resource group|
|`Role associated with Catalog`|`ibm_watsonx_data_catalog_role`|Role associated with Catalog|
|`Schema in the Presto Server`|`ibm_watsonx_data_schema`|Schema in the Presto Server|
|`Service instance` | `ibm_service_instance` | The service instance segment identifies the instance that the metric is associated with. |
{: caption="Table 14: Additional attributes" caption-side="top"}
