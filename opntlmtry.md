---

copyright:
  years: 2022, 2025
lastupdated: "2025-12-02"

keywords: watsonx.data, OpenTelemetry, traces, metrics, observability, Presto (Java), Presto (C++), Milvus

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


# OpenTelemetry
{: #opntlmtry}

OpenTelemetry is a highly customizable serviceability framework designed to enhance monitoring and debugging. It facilitates generation, collection, and management of telemetry data, such as traces and metrics, so you can visualize system behavior in observability dashboards.

- **Trace:** Represents the lifecycle of a single operation or request as it propagates through a system, capturing spans to detail its execution across services.
- **Metrics:** Provide numerical measurements that reflect the performance, health, or behavior of a system, such as request counts, error rates, or resource utilization over time.

OpenTelemetry is available only for the Presto (Java) engine in the {{site.data.keyword.lakehouse_full}} Enterprise edition, and only in the jp-tok region.

## Advantages
{: #opntlmtry_advantages}

- **Standardization:** Unifies collection and export of telemetry data, simplifying integration with observability tools and platforms.
- **Interoperability:** Provides common APIs and data formats for easy sharing of telemetry data across different systems and tools.
- **Flexibility:** Supports multiple languages and can be extended to cover custom telemetry needs, providing a flexible solution for a wide range of applications and environments.

## Related topics
{: #opntlmtry_related}

To learn more about adding telemetry diagnostic tools in {{site.data.keyword.lakehouse_short}}, explore the topics in [OpenTelemetry](/docs/watsonxdata?topic=watsonxdata-opntlmtry_ui_2.1.2).
