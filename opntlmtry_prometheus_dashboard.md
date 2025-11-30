---

copyright:
  years: 2022, 2025
lastupdated: "2025-11-30"

keywords: Grafana, Prometheus, OpenTelemetry, dashboards, Presto, Milvus

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


# Customizing Grafana dashboards to monitor engine performance
{: #opntlmtry_prometheus_dashboard}

Grafana dashboards provide a powerful and flexible way to visualize and monitor the performance and health of your Presto and Milvus engines. This guide outlines how to import default dashboards, apply filters, and customize them to suit your observability needs.

## Before you begin
{: #opntlmtry_prometheus_dashboard_byb}

Before importing dashboards, make sure:
- A Prometheus data source is configured in Grafana. Refer to [Grafana data sources](https://www.ibm.com/links?url=https%3A%2F%2Fgrafana.com%2Fdocs%2Fgrafana%2Flatest%2Fdatasources%2F){: external} documentation.
- Required metrics are available from the data source.

## Procedure
{: #opntlmtry_prometheus_dashboard_steps}

Follow the steps to create default dashboards in Grafana UI for **OpenTelemetry** data:

1. **Importing the default JSON template**
   You can import a predefined JSON dashboard template downloaded from [Milvus](https://www.ibm.com/docs/en/SSDZ38_2.2.x/lh-over/topics/MilvusDashboards.zip){: external} and [Presto](https://www.ibm.com/docs/en/SSDZ38_2.2.x/lh-over/topics/PrestoDashboards.zip){: external} using the following method:

   - After downloading the JSON dashboard template:
     1. In the Grafana UI, navigate to **Home → Dashboards → New → Import Dashboard**.
     2. Upload the dashboard JSON file.
     3. Select the appropriate Prometheus data source.
     4. After import, configure the filter **instanceId** by selecting the `instance_id` from the drop-down and **EngineId** by selecting the engine ID (labeled as `podUid`) for your engine.

2. **Adding filters or Grafana variables**
   To add a new variable:
   1. Open the dashboard.
   2. Click the **gear icon** and select **Dashboard Settings**.
   3. Navigate to **Variables** and select **Add variable**.
   4. Choose a variable type from the list (**Query**, **Custom**, **Constant**).
   5. Update the required fields and save.

   Refer to [Grafana Variables](https://www.ibm.com/links?url=https%3A%2F%2Fgrafana.com%2Fdocs%2Fgrafana%2Flatest%2Fdashboards%2Fvariables%2F){: external} for information.
   {: note}

3. **Customizing dashboards**
   You can modify dashboard panels to better visualize your data:
   - Add new panels with custom queries and visualizations.
   - Edit existing panels to change metrics, queries, or visual settings.
   - Rearrange panels for clarity.
   - Update legends and labels.

   Refer to [Grafana Build dashboards](https://www.ibm.com/links?url=https%3A%2F%2Fgrafana.com%2Fdocs%2Fgrafana%2Flatest%2Fdashboards%2Fbuild-dashboards%2F){: external} for information.
   {: note}
