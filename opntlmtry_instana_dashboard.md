---

copyright:
  years: 2022, 2025
lastupdated: "2025-12-01"

keywords: Instana, OpenTelemetry, dashboards, Presto, Milvus, customization

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


# Customizing Instana dashboards to monitor engine performance
{: #opntlmtry_instana_dashboard}

IBM® Instana Observability dashboards provide a comprehensive view of the performance and health of your Presto (Java) and Presto (C++) engines. You can use these dashboards to monitor key metrics, diagnose issues, and optimize resource allocation. While default templates are available, you can customize them to gain deeper insights by adding widgets and metrics.

## Procedure
{: #opntlmtry_instana_dashboard_steps}

Follow the steps to create default dashboards in Instana UI for **OpenTelemetry** data:

1. **Importing the default JSON template**
   You can import a predefined JSON dashboard template using one of the following methods:

   - **If you have a JSON template file:**
     1. Navigate to Instana home page.
     2. Select **Custom Dashboards** from the left-hand panel.
     3. Click **Create New Dashboard**.
     4. Provide a suitable name for the dashboard. A blank dashboard page will appear.
     5. Click on the **Options** menu and select **Edit as JSON**.
     6. Paste the JSON template into the editor.
     7. Update the dashboard name if needed, then save your changes.

   - **Importing from central registry:**
     Instana templates specific for {{site.data.keyword.lakehouse_full}} by creating buckets are hosted in the central registry at [instana-integration (Packages)](https://www.ibm.com/links?url=https%3A%2F%2Fwww.npmjs.com%2Forg%2Finstana-integration){: external}.

     To import from the central registry, refer to the [Instana documentation on importing dashboards](https://www.ibm.com/docs/en/instana-observability/current?topic=preview-unleashing-your-instana-observe-new-technologies#importing-the-dashboards){: external}.

2. **Filtering for a specific engine**
   Once the dashboard is populated, you can focus on a specific engine within an instance by applying filters:

   - Click on the filter option in the dashboard.
   - Add the following filters:
     - `metric.tag.Instanceid`: Enter the desired {{site.data.keyword.lakehouse_short}} instance ID.
     - `metric.tag.PodUid`: Enter the engine ID to filter data for a specific engine.

   These filters help isolate metrics relevant to the selected engine within the chosen instance.
   {: note}

3. **Customizing dashboards**
   To customize the default dashboards in Instana by adding additional metrics and widgets, refer to the official documentation:

   - [Building Custom Dashboards in Instana](https://www.ibm.com/docs/en/instana-observability/current?topic=instana-building-custom-dashboards){: external}
   - [Integration package management](https://www.ibm.com/docs/en/instana-observability/current?topic=opentelemetry-integration-package-management-public-preview){: external}
