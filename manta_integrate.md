---

copyright:
  years: 2022, 2025
lastupdated: "2025-07-16"

keywords: watsonx.data, spark, emr
subcollection: watsonxdata

---

{{site.data.keyword.attribute-definition-list}}

# Integrating with IBM Manta Data Lineage
{: #manta_integrate}

Integrating Manta with {{site.data.keyword.lakehouse_short}} allows you to capture and publish jobs, runs, and dataset events from Spark and Presto through the Manta UI, providing full visibility into data flows and transformations.
{: shortdesc}

Manta Data lineage is not supported with the Lite Presto (Java) engine in Lite plan instances.
{: note}

## Before you begin
{: #manta_integrate_prereq}

- Create a data source definition and an OpenLineage connection.
- Create an OpenLineage metadata import in your project and run it.

For more information, see [Preparing data for IBM Manta Data Lineage](https://dataplatform.cloud.ibm.com/docs/content/wsj/lineage/add-data-lineage.html?audience=wdp&context=cpdaas).

## Procedure
{: #manta_integrate_pros}

1. Log in to the watsonx.data console.
1. From the navigation menu, go to **Configurations** > **IBM Manta Data Lineage**.
1. Enter the following details:

   | Field | Description |
   | --- | --- |
   | Lineage ingestion endpoint | Enter the {{site.data.keyword.cloud_notm}} host endpoint URL where the data lineage service is activated. |
   | API key | Enter the API key. For information about generating an API key, see [Creating an API key](https://dataplatform.cloud.ibm.com/docs/content/wsj/admin/admin-apikeys.html?audience=wdp&context=cpdaas#creating-an-api-key) |
   {: caption="IBM Manta Data Lineage integration" caption-side="bottom"}

1. Click **Save** to save the details. You can edit the saved details by clicking **Edit**.
1. Click **Enable** to enable Manta Data Lineage.

Data lineage takes effect for new jobs that are started after enabling it. Previous and ongoing jobs will not display data lineage. Currently, it supports viewing lineages for CREATE TABLE AS (CTAS) and INSERT INTO SELECT operations in Manta Data Lineage.
{: note}

## What to do next
{: #manta_integrate_postreq}

- You can view data lineage for your assets. For more information, see [Viewing data lineage](https://dataplatform.cloud.ibm.com/docs/content/wsj/lineage/create-lineage.html?audience=wdp&context=cpdaas).
- You can manage and adjust your lineage graph to get comprehensive visibility and control of the data pipeline. For more information, see [Managing data lineage graph](https://dataplatform.cloud.ibm.com/docs/content/wsj/lineage/manage-lineage.html?audience=wdp&context=cpdaas).
