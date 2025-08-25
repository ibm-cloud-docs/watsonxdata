---

copyright:
  years: 2022, 2025
lastupdated: "2025-08-25"

keywords: lakehouse, watsonx data, roles, access
subcollection: watsonxdata

---

{:javascript: #javascript .ph data-hd-programlang='javascript'}
{:java: #java .ph data-hd-programlang='java'}
{:ruby: #ruby .ph data-hd-programlang='ruby'}
{:php: #php .ph data-hd-programlang='php'}
{:python: #python .ph data-hd-programlang='python'}
{:external: target="_blank" .external}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:tip: .tip}
{:important: .important}
{:note: .note}
{:deprecated: .deprecated}
{:pre: .pre}
{:video: .video}

# Billing and usage
{: #manage_bill}

Billing in {{site.data.keyword.lakehouse_full}} is based on the charge metrics that are defined by {{site.data.keyword.Bluemix_short}} service.
{: shortdesc}

The following charge matrices apply to {{site.data.keyword.lakehouse_short}}:

* Resource Unit (RU): A measure of resources managed, processed, or related to the use of {{site.data.keyword.lakehouse_short}} service instance. Here, compute and support services are considered resources.

* Compute cluster: Consists of coordinator and worker nodes that run the query engine. Each node consumes a set of resource units per hour (as defined by the {{site.data.keyword.Bluemix_short}}) until the node is paused or deleted.

* Support services: Consists of supporting services such as metadata storage and access control.


## Metering and billing granularity in {{site.data.keyword.lakehouse_short}}
{: #manage_bill1}

Billing is based on the the total run rate, which is the sum of the individual run rates of all the infrastructure components currently running in your instance. The resource unit consumption begins as soon as you create a watsonx.data instance, when the support services are available and continue until you delete the instance.

You can view the estimate of the expected per-hour run rate consumption of **Resource Units** from the **About** tab in the [**{{site.data.keyword.lakehouse_short}}** **{{site.data.keyword.Bluemix_short}} catalog**](https://cloud.ibm.com/watsonxdata) page.

Important: **watsonx.data is metered on a per-second basis to ensure precise and granular tracking of usage.**
This fine-grained metering allows for greater transparency and control, capturing every second the instance is active, regardless of whether any engine is enabled. While billing is aggregated and performed hourly, the underlying usage data is collected per second and sent to IBM Cloud. This continuous per-second metering ensures that charges reflect actual usage time. To avoid incurring unnecessary costs, it is important to delete unused instances promptly.

For example:

**Scenario 1: Presto C++ starter instance usage**

You create a {{site.data.keyword.lakehouse_short}} instance configured with Presto C++ starter, which includes:

1 co-ordinator node, 1 worker node, and support services enabled.

The following table displays the metering calculation when you run the instance for 14 minutes 30 seconds.
The usage time which, is monitored in seconds will be internally converted to hours. Here, 0.2416 hours.

| Component |  Runtime calculation(in seconds (s)) \n Metering | Runtime calculation (in hours (h)) \n Billing | Unit Price (1RUs/h = $1USD) | Total Price (1 RU = $1.00 USD)|
| --- | --- | -- | ---| ---|
| Presto C++ starter with 1 coordinator |  (14 * 60) s + 30 s = 870 s| (870/3600) h |1.5 RU| 0.2416 h * 1.5 RU = 0.3652 RU =$0.3652 USD|
| Presto C++ starter with 1 worker node| (14 * 60) s + 30 s = 870 s| (870/3600) h | 1.5 RU | 0.2416 h * 1.5 RU = 0.3652 RU =$0.3652 USD|
| Supporting services | (14 * 60) s + 30 s = 870 s | (870/3600) h |  3 RU| 0.2416 h * 3 RU = 0.725 RU = $0.725 USD|
|Total | 1740 s| 0.4833 h |6RUs|1.4496 RU = $1.4496 USD|
{: caption="Presto C++ starter instance usage calculation" caption-side="bottom"}


**Scenario 2: Instance with Presto C++ starter and Milvus t shirt**


You create a {{site.data.keyword.lakehouse_short}} instance with the following configuration:

Presto C++ starter: Includes, 1 co-ordinator and 1 worker node (both starter size), Milvus t-shirt size, and support services enabled.

The following table displays the metering calculation when you run the instance  for a total of 35 minutes and 30 seconds but Presto C++ runs for only the first 14 minutes and 30 seconds.

| Component |  Runtime calculation(in seconds (s)) \n Metering | Runtime calculation (in hours (h)) \n Billing |Unit Price (1RUs/h = $1.00 USD) | Total Price (1 RU = $1.00 USD)|
| --- | --- | -- | ---| ---|
| Presto C++ starter with 1 coordinator |  (14 * 60) s + 30 s = 870 s| (870/3600) h |1.5 RU| 0.2416 h * 1.5 RU = 0.3652 RU =$0.3652 USD|
| Presto C++ starter with 1 worker node| (14 * 60) s + 30 s = 870 s| (870/3600) h | 1.5 RU | 0.2416 h * 1.5 RU = 0.3652 RU =$0.3652 USD|
| Milvus t-shirt size| (14 * 60) s + 30 s = 870 s| (870/3600) h | 1.25 RU | 0.2416 h * 1.25 RU = 0.302 RU =$0.302 USD|
| Supporting services | (35 * 60) s + 30 s = 2130 s | (2130/3600) h |  3 RU| 0.592 h * 3 RU = 1.775 RU = $1.775 USD|
|Total | 4740 s| 1.3166 h |7.25RUs|2.807 RU = $2.807 USD|
{: caption="Presto C++ starter instance usage calculation" caption-side="bottom"}


The **Billing and Usage** page provides the latest information about RU consumption breakdown of the instance (based on the resource utilization).

To view current billing and usage details, complete the following steps:

1. Log in to the {{site.data.keyword.lakehouse_short}} console.

1. From the navigation menu, select **Billing and usage**. The **Billing and usage** page opens.

    The **Total run rate** field displays the sum of the run rates of all currently running infrastructure components in the instance.

    The billable infrastructure components are listed in the table. You can also type the component name in the **Search** field to list a particular component.

1. Click the **Customize columns** icon and select the columns to display.

1. Click the **Manage resource usage** link. The [IBM Cloud Billing and usage](https://cloud.ibm.com/billing) page opens.

The following are the fields in the **Billing and usage** page:

| Field           | Description        |
|------------------|--------------------|
| Display name     | The name of the billable component. |
| Status      | The status of the component. It can be running, failed, provisioning, restarting, resuming, scaling, updating, or paused. The **Running** status displays a run rate above 0 RUs/hour. |
| Component type            | The category of the component. |
| Run rate             | The resource units that are consumed per hour. |
{: caption="Billing and usage" caption-side="bottom"}
