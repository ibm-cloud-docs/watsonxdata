---

copyright:
  years: 2017, 2022
lastupdated: "2024-09-10"

subcollection: AnalyticsEngine

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}


# Default limits and quotas for Spark engine
{: #wxd-ae_limits}

The following sections provide details about the default limit and quota settings for the Spark engine.
{: shortdesc}

These default values are set to avoid excessive billing, to override the default limits and quotas for the Spark engine, based on your requirements, contact IBM Support.
{: note}

## Application limits
{: #limits_application}

The following table lists the default limits and quotas for the Spark engine.


| Category                                |        Default         |
| --------------------------------------- | ---------------------- |
| Maximum number of Spark engines per watsonx.data instances |                      3 |
| Maximum number of nodes per Spark engine              |                    20 |
| Shuffle space per core                  | approx. 30 GB (Not customizable) |
{: caption="Default limits and quotas for Spark instances" caption-side="top"}


## Supported Spark driver and executor vCPU and memory combinations
{: #cpu-mem-combination}

Apache Spark supports only the following pre-defined Spark driver and executor vCPU and memory combinations.

These two vCPU to memory proportions are supported: 1 vCPU to 4 GB of memory and 1 vCPU to 8 GB of memory.

The following table shows the supported vCPU to memory size combinations.

| Lower value | Upper value |
| ------------|-------------|
| 1 vCPU x 1 GB | 10 vCPU x 48 GB |
{: caption="Supported vCPU to memory size combinations" caption-side="top"}
