---

copyright:
  years: 2017, 2025
lastupdated: "2025-12-09"

keywords: watsonx.data, spark, analytics, provisioning
subcollection: watsonxdata

---

{{site.data.keyword.attribute-definition-list}}

# Managing Spark engine capacity
{: #mng_capacity_spk}


**Applies to** : [Spark engine]{: tag-blue}  [Gluten accelerated Spark engine]{: tag-green}

The **Capacity** tab in a Spark engine instance provides a comprehensive view of overall CPU and memory utilization, helping you monitor resource consumption effectively. By default, you can enjoy a serverless engine experience, which automatically scales resources based on workload demands. Additionally, for large-scale or high-performance workloads, you have the flexibility to allocate dedicated capacity, ensuring optimal performance and reliability.


## Key features
{: #mng_capacity_key}

* Each Spark engine can attach to multiple reservation pools (node pools with different flavors).
* Dedicated Workloads with Autoscaling: A dedicated environment provides users with their own reserved compute capacity, ensuring consistent performance and control. When combined with autoscaling, users get the best of both reliability and efficiency.
* Quotas will be enforced for both Dedicated and On-Demand capacity.
* For users who frequently run large or long jobs, it is recommended to attach Dedicated Capacity for predictable performance.

## Serverless Spark
{: #mng_capacity_serv}

* Pay-per-use cost model: Customers only pay for the compute resources consumed when workloads run. This avoids paying for idle capacity when usage is intermittent or low.
* Automatic scaling: Serverless platforms automatically scale resources up or down based on demand, eliminating the need for manual provisioning or capacity planning.
* No infrastructure management: The platform handles patching, scaling, and maintenance, reducing operational overhead.
* Fast time-to-value: Customers can deploy quickly without upfront planning or infrastructure sizing.

## Benefits of having Dedicated capacity with autoscaling
{: #mng_capacity_aut}


* Stable baseline performance: Dedicated capacity ensures that workloads with long-running or continuous usage have guaranteed compute resources without competition.

* Efficient scaling for peak demand: Autoscaling layers on top of the dedicated baseline to automatically add more capacity when usage spikes, ensuring performance is maintained even during unexpected surges.

* Cost-optimized for sustained workloads: Customers pay for dedicated resources that they rely on consistently, while autoscaling prevents over-provisioning by only adding extra capacity when required.

* Operational flexibility: Teams can configure both the minimum dedicated capacity for continuous workloads and an upper autoscaling cap to control spend.

* Improved reliability: Scaling events happen automatically, reducing downtime risk and ensuring services handle fluctuating workloads without manual intervention.



## Before you begin
{: #mng_capacity_bfb}

To experience this feature, you must use version 2.3(and above) of {{site.data.keyword.lakehouse_short}}.


## Viewing and configuring capacity details
{: #mng_capacity_view}

To view the capacity tab, do the following:

1. Log in to the {{site.data.keyword.lakehouse_short}} console.
1. Navigate to **Infrastructure manager**. Click the Spark engine.
1. Click **Capacity** tab. You can view the following sections:

   * **Overall Usage Metrics**: Displays total vCPUs and memory allocated, along with real-time CPU and memory consumption percentages.
   * **Dedicated**: Dedicated capacity for large workloads. It displays details of configured capacity pools, including vCPU and memory allocation, consumption levels, and options to manage pools (add, edit, pause, or delete).
   * **On-Demand**: When a Spark engine is created, it automatically provides on-demand capacity—this is the default serverless option that scales resources dynamically based on workload requirements. It displays the memory consumption for your applications.


## On-demand Spark engine capacity
{: #on-demnd}

On-Demand Capacity is the default serverless execution model for Spark engines, designed to provide flexibility and simplicity without requiring upfront resource planning. When a Spark engine is created, it automatically includes on-demand capacity, enabling workloads to run. Resources are provisioned dynamically based on workload requirements, automatically scale them upto the maximum number of cores available for on-demand capacity within a Spark engine as specified.

To update the On-Demand capacity quota,

From the **Capacity** tab, click **On-demand**. Click **Edit quota**. A horizontal slider lets you select the desired capacity quota (in cores) within the allowed range (0 to 100 cores). Click **Save**.

For example, when you set the quota to 40 cores, the engine automatically scales resources up to that limit based on workload demands. To scale beyond 100 cores, you have to reach out to IBM Support.

## Creating a dedicated capacity for your workload
{: #dedictaed}

Dedicated capacity provides a way to reserve compute resources for Spark workloads, ensuring predictable performance and cost stability for large or long-running jobs. Unlike On-Demand Capacity, which scales dynamically, dedicated capacity allows you to attach reservation pools with specific configurations to your Spark engine.

* Each Spark engine can attach upto three capacity pools with different flavors, enabling flexibility for diverse workload requirements.
* Dedicated Capacity supports minimum and maximum node pool settings, giving you control over resource allocation and scaling boundaries.
* If Dedicated Capacity is attached, workloads run on it by default. If no Dedicated Capacity is available, workloads fall back to On-Demand Capacity automatically.


To add a dedicated capacity pool for your spark workloads:

From the **Capacity** tab, click **Dedicated** tab. Click **Add node pool+**. The **Edit flavour(dedicated)** page opens. Provide the following details:


1. Provide a name for the configuration in the **Instance type name** field.

1. Select the required memory combination from the **Select flavour** list. The following configurations are available.

   | Flavour Type      | Flavour     | Core | Memory (GB) | Usable Core | Usable Memory (GB) | Shuffle Storage per Core (GB) | Secondary Storage (GB / Tier)                    |
   |-------------------|-------------|------|--------------|--------------|--------------------|-------------------------------|--------------------------------------------------|
   | General Purpose   | bx2.16x64   | 16   | 64           | 14           | 60                 | 50                            | 900 GB / 10 IOPS-tier                           |
   | General Purpose   | bx2.32x128  | 32   | 128          | 30           | 124                | 50                            | 1600 GB / 10 IOPS-tier                          |
   | Memory Intensive  | mx2.16x128  | 16   | 128          | 14           | 124                | 50                            | 900 GB / 10 IOPS-tier                           |
   | Memory Intensive  | mx2.32x256  | 32   | 256          | 30           | 252                | 50                            | 1600 GB / 10 IOPS-tier                          |
   | Storage Intensive | mx2.16x128  | 16   | 128          | 14           | 124               | 100                           | 1600 GB / 10 IOPS-tier                          |
   | Storage Intensive | mx2.32x256  | 32   | 256          | 30          | 252                | 100                           | 3000 GB / 10 IOPS-tier |
   {: caption="Memory configurations" caption-side="bottom"}

1. Specify the **Minimum nodes** and **Maximum nodes** required for scaling. Dedicated capacity supports minimum and maximum node pool settings, giving you control over resource allocation and scaling boundaries.

1. Select the **Set as default capacity** to choose this configuration as the default capacity for your selected Spark engine.

1. Click **Save**.
