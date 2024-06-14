---

copyright:
  years: 2022, 2024
lastupdated: "2024-05-31"

keywords: watsonx.data, ikc, configuring, knowledgecatalog
subcollection: watsonxdata

---

{{site.data.keyword.attribute-definition-list}}

# Integrating with IBM Knowledge Catalog (IKC)
{: #ikc_integration}

Integrating {{site.data.keyword.lakehouse_full}} with IBM Knowledge Catalog (IKC) provides self-service access to data assets for knowledge workers who need to use those data assets to gain insights.

## Before you begin
{: #prereq_ikc}

For Enabling IKC Integration, ensure to have the following prerequisites.

- A working {{site.data.keyword.lakehouse_short}} environment.
- A working IBM Knowledge Catalog (IKC) environment.
- Make sure that IBM Knowledge Catalog and {{site.data.keyword.lakehouse_short}} are configured with service-to-service authorization in {{site.data.keyword.Bluemix_notm}}.

<!-- Confirm the content, add to a topic, and hyperlink in the above service to service authorization -->

## Connect and import the table metadata from  {{site.data.keyword.lakehouse_short}} to WKC
{: #connect_import}
{: step}

1. Log in to {{site.data.keyword.Bluemix_notm}}.
1. Go to **Resource list** > **AI / Machine Learning** > **IBM Knowledge Catalog**.
1. Click **Launch in IBM Cloud Pak for Data**. The IBM Knowledge Catalog home page opens.
1. From the left pane, go to **Catalogs** > **View all catalogs**. The **Catalogs** page opens with the list of available catalogs.
1. To create a new catalog:
    1. Click **New catalog**.
    1. In the **New catalog** page:
        - In the **Name** field, add a name for the catalog.
        - In the **Description** field, add a description.
        - Select the **Enforce data protection and data location** rules checkbox. <!-- What about other fields in the page? -->
    1. Click **Create**. The catalog is created and the catalog page opens.
1. Go to **Add to catalog** > **Connection**.
1. In the **New connection** page, search and select {{site.data.keyword.lakehouse_full}}.
1. Enter the following details:
   | Field | Description |
   |-------|-------------|
   | Hostname or IP address | Enter the hostname or IP address. |
   | Port | Enter the port number. |
   | Instance ID | Enter the instance ID. |
   | Instance name | Enter the instance name. |
   | CRN | Enter the same value as instance ID. |
   | Username | Enter your username. |
   | Password | Enter your password. |
   | Mask sensitive credentials retrieved through API calls | *TBD what's the use of this?* |
   | Validate the SSL certificate | Make sure that the checkbox is not selected. |
   | SSL is enabled | Select the checkbox. *add the purpose of this* |
   | Engine's hostname or IP address | Enter the engine hostname available in the {{site.data.keyword.lakehouse_short}} UI. |
   | Engine ID | Enter the engine ID available in the {{site.data.keyword.lakehouse_short}} UI. |
   | Engine's port | Enter the engine port number. |
   {: caption="Table 1. New connection" caption-side="bottom"}

1. Click **Test connection** to test the connection.
1. Click **Create**. The connection is added to the catalog.
1. Go to **Add to catalog** > **Connected assets**.
1. In the connected asset, click **Select source** and navigate to the table you want to import.
1. Select the table and click **Add**. The table asset is successfully added to IKC.

<!-- I haven't added the rest of the steps, need clarity on each of the tabs to document. -->

## Configure IKC in {{site.data.keyword.lakehouse_full}} UI
{: #conf_ikc}
{: step}

1. Log in to {{site.data.keyword.lakehouse_full}}.
1. From the left pane, go to **Access control**.
1. Select the catalog to open the catalog details page.
1. Go to the **Integrations** tab and click **Integrate service**.
1. Enter the following details:
   | Field | Description |
   |-------|-------------|
   | Service | Select **Watson Knowledge Catalog**. |
   | Bucket catalogs | Select the applicable bucket catalogs for IKC governance. |
   | WKC endpoint  | Configure the IKC API url |
   {: caption="Table 1. Ingrate service" caption-side="bottom"}

1. Click **Integrate**.

## Verify the masking functionality as per the rules in IKC
{: #verify_mask}
{: step}

1. Login to IBM Knowledge Catalog. <!-- Should we provide more details? -->
1. From the left pane, go to **Governance** > **Rules**.
1. From the **Rules** page, verify that the rules corresponding to your data class of the column is defined. You can define a new rule using **Add rule** button. <!-- Should we provide more details about the procedure? -->

The owner can see the unmasked data
{: note}

## Supported datatypes
{: #datatypes_supported}

{{site.data.keyword.lakehouse_full}} IKC integration supports the following datatypes:

- Varchar
- Bigint
- Boolean
- Date
- Double
- Integer
- Smallint
- Timestamp
- Tinyint
