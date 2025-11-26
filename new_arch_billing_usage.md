---

copyright:
  years: 2022, 2025
lastupdated: "2025-11-26"

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

# Metering and usage experience
{: #manage_bil_newarch}

The metering service in {{site.data.keyword.lakehouse_full}} provides users with real-time visibility on engine consumption and resource usage. The Billing and Usage screen provides a comprehensive view of resource consumption and cost metrics for your instance. It helps you monitor billable infrastructure components, and track Resource Unit (RU) usage.
{: shortdesc}

It captures engine session runtime, engine type with T-shirt size, and hourly Resource Unit (RU) usage data, creating a unified view that helps you track usage, understand costs, and optimize resources.


The following charge matrices apply to {{site.data.keyword.lakehouse_short}}:

* Resource Unit (RU): A measure of resources managed, processed, or related to the use of {{site.data.keyword.lakehouse_short}} service instance. Here, compute and support services are considered resources.

* Compute cluster: Consists of coordinator and worker nodes that run the query engine. Each node consumes a set of resource units per hour (as defined by the {{site.data.keyword.Bluemix_short}}) until the node is paused or deleted.

* Support services: Consists of supporting services such as metadata storage and access control. Metering for support services starts when you launch the instance and initiate the Quick Start step, and continue until you delete the instance.


## Runtime-Level metering
{: #manage_run}

Metering is now performed at the runtime level, capturing start, stop, and pause events for each runtime tied to an engine.
Presto Engines: One-to-one mapping (single runtime per engine).
Spark Engines: Multiple runtimes per engine, including subtypes like:

* Kernel
* HistoryServer
* Application
* Each Spark application creates a new runtime, and active/inactive hours are tracked individually.

## Features for metering
{: #manage_run_activity}

Runtime activity bars display active and inactive hours per runtime. The View History links are scoped to the runtime level for detailed event tracking.
The UI captures start and end timestamps for every engine session (Presto++, Spark, Milvus, Gluten).
Record engine type and T-shirt size (S/M/L) for pricing alignment.
Provide hourly RU usage data for billing reference.


## Reporting considerations
{: #manage_report}

Total usage: It is the sum of individual usage of all the infrastructure components running in the instance for the current month.
Total hourly usage:       .
Usage history per engine:    .

## Viewing the usage details

To view current billing and usage details, complete the following steps:

1. Log in to the {{site.data.keyword.lakehouse_short}} console.

1. From the navigation menu, select **Billing and usage**. The **Billing and usage** page opens. You can view the following:


   * **Total usage**

   It displays the aggregate RU consumption for the current calendar month.
   Usage Bar:

      * Active RUs (Green): Shows RUs consumed during active engine runtime.

      * Idle RUs (Yellow): Indicates RUs consumed while engines were idle.

   Example: 9.75 RUs total, with 7 RUs active and 2.75 RUs idle.

   * **Billable Components Table**

   Lists all engines and services contributing to usage.

   | Field           | Description        |
   |------------------|--------------------|
   | Display name     | The name of the billable component. |
   |Type          | Engine type (Presto, Spark, Milvus, etc.).|
   |Size.  | T-shirt size (Small, Medium, Large).|
   | Status      | The status of the component. It can be running, failed, provisioning, restarting, resuming, scaling, updating, or paused. The **Running** status displays a run rate above 0 RUs/hour. |
   | Total Usage (RUs)            | Cumulative RU consumption. |
   | Total Uptime             | Duration the component was active. |
   | Owner.  |   Associated user or team.|
   {: caption="Billing and usage" caption-side="bottom"}

   When you select an engine (e.g., Presto Java), you can view the detailed metrics:

   Usage:
   Active RUs vs Idle RUs breakdown.

   Runtime:

   Uptime and Downtime durations displayed with color-coded bars.
   Example: Uptime: 1 hour 10 min, Downtime: 1 hour.

   * **Total Hourly Usage**

   Visual representation of RU consumption across hours and days.

   Color Intensity: Darker shades indicate higher usage.

   Helps identify peak usage periods for optimization.

   * **Usage History per Engine**

   Line chart showing RU usage trends for individual engines over time. Multiple Engines: Each engine represented by a different color line. Enables comparison of usage patterns across engines.



## Metering and billing granularity in {{site.data.keyword.lakehouse_short}}
{: #manage_bill1}

Billing is based on the the total run rate, which is the sum of the individual run rates of all the infrastructure components currently running in your instance.
Resource unit consumption begins as soon as Support Services are activated with the initiation of Quick Start step and continues until the instance is deleted.



You can view the estimate of the expected per-hour run rate consumption of **Resource Units** from the **About** tab in the [**{{site.data.keyword.lakehouse_short}}** **{{site.data.keyword.Bluemix_short}} catalog**](https://cloud.ibm.com/watsonxdata) page.

Important: **watsonx.data is metered on a per-second basis to ensure precise and granular tracking of usage.**

This fine-grained metering allows for greater transparency and control, capturing every second the instance is active, regardless of whether any engine is enabled. While Usage and Billing collection is aggregated and updated on IBM Cloud at an hourly basis, the underlying metering collection is done at a per second basis. This continuous per-second metering ensures that charges reflect actual usage time. To avoid incurring unnecessary costs, it is important to delete unused instances promptly.

For example:

**Scenario 1: Presto C++ starter instance usage**

You create a {{site.data.keyword.lakehouse_short}} instance configured with Presto C++ starter, which includes:

Presto C++ starter, and support services enabled.

The following table displays the metering calculation when you run the instance for 14 minutes 30 seconds.
The usage time which, is monitored in seconds will be internally converted to hours. Here, 0.2416 hours.

| Component |  Runtime calculation(in seconds (s)) \n Metering | Runtime calculation (in hours (h)) \n Billing | Unit Price (1RUs/h = $1USD) | Total Price (1 RU = $1.00 USD)|
| --- | --- | -- | ---| ---|
| Presto C++ starter with 1 coordinator |  (14 * 60) s + 30 s = 870 s| (870/3600) h |1.5 RU| 0.2416 h * 1.5 RU = 0.3652 RU =$0.3652 USD|
| Presto C++ starter with 1 worker node| (14 * 60) s + 30 s = 870 s| (870/3600) h | 1.5 RU | 0.2416 h * 1.5 RU = 0.3652 RU =$0.3652 USD|
| Supporting services | (14 * 60) s + 30 s = 870 s | (870/3600) h |  3 RU| 0.2416 h * 3 RU = 0.725 RU = $0.725 USD|
|Total | 1740 s| 0.4833 h |6RUs|1.4496 RU = $1.4496 USD = $1.45 USD|
{: caption="Presto C++ starter instance usage calculation" caption-side="bottom"}


**Scenario 2: Instance with Presto C++ starter and Milvus starter**


You create a {{site.data.keyword.lakehouse_short}} instance with the following configuration:

Presto C++ starter, Milvus starter size and support services enabled.

The following table displays the metering calculation when you run the instance  for a total of 35 minutes and 30 seconds but Presto C++ runs for only the first 14 minutes and 30 seconds.

| Component |  Runtime calculation(in seconds (s)) \n Metering | Runtime calculation (in hours (h)) \n Billing |Unit Price (1RUs/h = $1.00 USD) | Total Price (1 RU = $1.00 USD)|
| --- | --- | -- | ---| ---|
| Presto C++ starter with 1 coordinator |  (14 * 60) s + 30 s = 870 s| (870/3600) h |1.5 RU| 0.2416 h * 1.5 RU = 0.3652 RU =$0.3652 USD|
| Presto C++ starter with 1 worker node| (14 * 60) s + 30 s = 870 s| (870/3600) h | 1.5 RU | 0.2416 h * 1.5 RU = 0.3652 RU =$0.3652 USD|
| Milvus starter| (14 * 60) s + 30 s = 870 s| (870/3600) h | 1.25 RU | 0.2416 h * 1.25 RU = 0.302 RU =$0.302 USD|
| Supporting services | (35 * 60) s + 30 s = 2130 s | (2130/3600) h |  3 RU| 0.592 h * 3 RU = 1.775 RU = $1.775 USD|
|Total | 4740 s| 1.3166 h |7.25RUs|2.807 RU = $2.807 USD = $2.81 USD|
{: caption="Presto C++ starter instance usage calculation" caption-side="bottom"}
