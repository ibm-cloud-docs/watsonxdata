---

copyright:
  years: 2022, 2025
lastupdated: "2025-12-01"

keywords: watsonx.data, OpenTelemetry, telemetry, diagnostics, Instana, Prometheus, Grafana

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


# Adding telemetry diagnostic tools through the user interface
{: #opntlmtry_ui_2.1.2}

This topic provides the procedure to add telemetry diagnostic tools for your Presto (Java) and Presto (C++) engines through the user interface of {{site.data.keyword.lakehouse_full}}.

## Before you begin
{: #opntlmtry_ui_2.1.2_byb}

Ensure you have access to the {{site.data.keyword.lakehouse_short}} console and credentials for the telemetry tools (Instana or Prometheus).

## Procedure
{: #opntlmtry_ui_2.1.2_steps}

1. Log in to the {{site.data.keyword.lakehouse_short}} console.

2. From the navigation menu, select **Configurations**, and click **OpenTelemetry**.

3. In the **OpenTelemetry** page, click **Diagnostic +**.

4. In the **Add telemetry diagnostic** window, enter the following details:

   | Field                   | Description                                                                                                                                                                                                 |
   |-------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
   | **Available Telemetry Tools** | Select the telemetry diagnostic tool (Instana, Prometheus) from the list.                                                                                                                              |
   | **Telemetry Endpoint**        | Enter the endpoint URL of the selected tool. Format: `http://<host>:<port>/<path>` or `https://<host>:<port>/<path>`. Use port `4317` for OTLP over GRPC and `4318` for OTLP over HTTP.             |
   | **Host Name**                  | If the selected telemetry tool is Instana, enter the host ID of the tool. See [Configuring the resource attributes](https://www.ibm.com/docs/en/instana-observability/1.0.302?topic=instana-backend#configuring-the-resource-attributes){: external}. |
   | **Password**                   | Enter the Instana agent key or Prometheus password.                                                                                                                                                   |
   | **TLS enabled**                | Use the **TLS enabled** toggle to secure the connection.                                                                                                                                              |
   | **Connection status**          | Click **Test connection** to validate the endpoint and credentials.                                                                                                                                  |
   | **Associated diagnostics**     | Select the checkbox to associate a diagnostic type (logs, metrics, traces) to the telemetry tool.   |
   {: caption="Add telemetry diagnostic details" caption-side="bottom"}

   Currently Instana provides only metrics and traces diagnostic data. Prometheus provides only metrics diagnostic data.
   {: note}

5. Click **Add** to apply the telemetry tool integration.

   The user may need to wait for a short time until the pods restart.
   {: note}

6. Access and review the diagnostics list of metrics for engines supported in your instance by using the drop-down menu to:
   - **Enable**: Activate the diagnostic.
   - **Disable**: Pause data collection.
   - **Edit**: Update configuration details.
   - **View Details**: Inspect current setup.
   - **Disassociate**: Remove the diagnostic from the engine.

   Once all supported diagnostic types have been successfully associated with any one or both telemetry tools, the **Add Diagnostic** button is disabled.
   {: note}

   To configure a new diagnostic tool or switch to another, you must either:
   - **Edit** the existing configuration.
   - **Disable** the current diagnostic.
   - **Disassociate** it.

### Checking telemetry data in Instana
{: #opntlmtry_ui_instana}

**To see traces generated for a query:**

1. Go to **Analytics** in the Instana UI and select **Services**.
2. Choose the relevant service: **presto** for Presto (Java) or **milvus.<podname>** for Milvus.
3. Filter traces by **Service Name**, **Call Name**, or **Retention Period** (last 5, 10, or 30 minutes).
4. Click on a specific trace to view details.

**To see metrics generated for a query:**

An Instana data source must be available.
{: important}

1. Go to **Analytics** → **Infrastructure** → **OpenTelemetry** in the Instana UI.
2. Choose the relevant service:
    - **`presto-jmx-<instance-id>`** (Presto Java)
    - **`prestissimo-jmx-<instance-id>`** (Presto C++)
    - **`milvus-<instance-id>`** (Milvus), where `<instance-id>` is your {{site.data.keyword.lakehouse_short}} instance ID.

3. Review the list of custom metrics and their attributes.
4. Click on a specific metric to view the live time series.

### Checking telemetry data in Grafana
{: #opntlmtry_ui_grafana}

To see metrics generated for a query:

A Prometheus and Grafana data source must be available, and Prometheus Remote Write receiver must be enabled using the flag `--web.enable-remote-write-receiver`.
{: important}

1. Select **Dashboards** from Grafana UI navigation menu and click **Add visualization**.
2. Choose **Prometheus** data source.
3. Select the Prometheus metrics you want to visualize from the query metric drop-down list.
4. Adjust the retention period to specify the time range for the metrics you want to view.
