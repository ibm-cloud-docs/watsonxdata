---

copyright:
  years: 2022, 2025
lastupdated: "2025-12-02"

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

This topic provides the procedure to add telemetry diagnostic tools for your Presto (Java) engine through the user interface of {{site.data.keyword.lakehouse_full}}.

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

### Navigate to Diagnostic Telemetry Data
{: #opntlmtry_ui_instana}

To review diagnostic telemetry (including internal and synthetic calls):

1. Log in to the Instana UI.
2. Navigate to **Analytics → Applications → Calls**.
3. In the left-side panel, locate the **Hidden calls** section.
4. Enable the following options:
   - **Show synthetic calls**
   - **Show internal calls**

This ensures that all internal, system-generated, and synthetic call data relevant to diagnostics is visible in the UI.

### Viewing traces for a specific query using CRN
{: #opntlmtry_ui_traces}

1. Go to **Analytics → Applications → Calls**.
2. Select **Add filter**.
3. In the filter search bar, type **OpenTelemetry → Custom → crn**.
4. Choose the **crn** attribute and set it to the desired `<crn_value>`.
5. Adjust the retention window to focus on recent trace activity:
   - Last 5 minutes
   - Last 10 minutes
   - Last 30 minutes

These retention periods help ensure recent query execution traces are visible without noise from older calls.

### Viewing OpenTelemetry metrics in Instana
{: #opntlmtry_ui_metrics}

1. Log in to the Instana UI and navigate to **Analyze Infrastructure**.
2. In the data source selector, choose **OpenTelemetry** to view all OpenTelemetry resources.
3. Click **Add filter**, select **OpenTelemetry Resource → otel.attribute → k8s.namespace.name**.
   Enter the required {{site.data.keyword.lakehouse_short}} instance namespace to filter the view.
4. From the filtered results, select the endpoint **metric-scraper-presto** associated with your instance.
5. Use **Select metrics** to browse all available OpenTelemetry metrics exposed by the Presto metric scraper.
6. Choose any metric to open its live time-series visualization, where you can analyze current values, trends, and attributes.

### Viewing Metrics in the Prometheus UI
{: #opntlmtry_ui_prometheus}

1. Access the Prometheus UI for your environment.
2. In the **Expression** field, begin typing the metric name (for example, `presto_`).
3. Prometheus will automatically display all metrics collected from **metric-scraper-presto**.
4. Select the required metric and click **Execute** to view the result.
