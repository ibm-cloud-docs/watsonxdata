---

copyright:
  years: 2022, 2024
lastupdated: "2024-10-08"

keywords: lakehouse, semantic automation, {{site.data.keyword.lakehouse_short}}, data enrichment, register

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

# Enriching data with semantic automation layer
{: #sal_enrichdata}

To enrich your data, {{site.data.keyword.lakehouse_full}} leverages Semantic Automation Layer (SAL) in IBM Knowledge Catalog.

Follow the procedure in this topic to enrich your data with business terms and descriptions using the semantic enrichment feature in {{site.data.keyword.lakehouse_short}}.

## Before you begin
{: #sal_enrichbyb}

- You have a registered semantic automation layer in {{site.data.keyword.lakehouse_short}}.
- You have a CSV file in a simplified format with the following fields:
   - Name: The business term you want to define.
   - Artifact Type: Always "glossary_term".
   - Description: The explanation of the business term.

   Sample file format:
   ```bash
   Name,Artifact Type,Description
   Residence Address,glossary_term,"Identifies an Address at which an Individual dwells, for example John Doe Resides At 102 Oak Court."
   Involved Party Markets Product Limit Condition,glossary_term,"Identifies a Limit Condition that applies to the Involved Party's marketing of the Product; for example, minimum audience or venues."
   Social Security Number,glossary_term,The unique number assigned to an Individual by a governmental agency for the purposes of qualifying for Social Security benefits.
   Rating Provider,glossary_term,"Identifies a Rating Issuer that supplies the Rating; for example, Credit Agency XYZ Provides Rating For a customer's Credit Risk Rating."
   ```
   {: codeblock}

## Procedure
{: #sal_enrichprcdre}

Users with the following roles can perform semantic enrichment in {{site.data.keyword.lakehouse_short}}:

   - **Admin or Metastore Admin**: These roles can register semantic automation layer and access the **Enrich Data** tab with all its functionality for data enrichment.
   - **User or Metastore Viewer**: These roles cannot view the **Configuration** tab for semantic automation layer registration or the **Enrich Data** tab. However, they can see any published enriched information, such as business terms and descriptions, when browsing data in the tables.

1. Log in to {{site.data.keyword.lakehouse_short}} console.
1. From the navigation menu, select **Data manager** and click **Enrich data** tab.
1. Click **Enrichment settings** and select **Manage glossary** to upload CSV file containing your business terms and descriptions.

   For the LLM to suggest tags and descriptions for the tables and columns in watsonx.data, upload a CSV file with your business terms (tags), artifacts type and their corresponding descriptions in the required format. The CSV file must conform the template as follows: Name, Artifact Type, Description as displayed in the UI.
   {: note}

1. In the **Manage glossary** window, click **Upload glossary** and drag the CSV file to the box or click to upload.
1. Select merge option:

   - **Replace all values**: Overwrites all existing tags and descriptions.
   - **Replace only defined values**: Replaces existing values only if the term exists in the uploaded file.
   - **Replace only empty values**: Adds tags and descriptions from the file only to columns without existing ones.

1. Click **Upload glossary**. The glossary displays a list of tags and its descriptions.
1. Click **Enrichment settings** and select **Adjust thresholds** to modify the thresholds for different types of enrichment. Click **Save all the changes**.

   The accuracy of semantic enrichment results for business terms largely depends on the IKC ability to match uploaded terms to the selected tables and columns. The threshold for suggestions can be adjusted to balance the matches with their confidence level. For more matches with potentially lower confidence, lower the threshold. For fewer matches with higher confidence, increase the threshold.
   {: note}

1. Select a schema that you want to enrich.

   For the Lite plan users, you can only enrich one schema from the list. After enriching a schema, other schemas can not be selected further. The enriched data will have the business terms and descriptions against each columns in each table inside the schema.
   {: note}

1. Click the overflow menu corresponding to the selected schema and select **Run enrichment**. You can also select single or multiple schemas and click **Enrich**.

1. Click the overflow menu next to the chosen schema and select **View enrichment**. The page displays the list of tables within the schema.
1. Click on any table to view details.
1. Assign business terms and descriptions manually:

   a. Hover over a business term and select **View more**, select **Governance** and click **Assign business terms**.

   b. Choose the relevant term from the uploaded glossary and click **Assign**.

1. Add display name and descriptions manually:

   a. Hover over a business term and select **View more**, select **Details** and click **Edit** icon.

   b. Modify the **Display name** or **Description** and click **Save**.

1. Review the enriched columns and click the overflow menu next to a column or **More** option and select **Mark as reviewed**.
1. Go to the table view and check if the review status is completed.
1. Click the overflow menu next to the chosen schema and select **Publish**. The page displays the list of enriched tables within the schema.
1. Verify the enriched data in the **Browse data** tab of the **Data Manager** by selecting the schema you enriched on successful completion of publishing.
