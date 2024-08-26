---

copyright:
  years: 2022, 2024
lastupdated: "2024-08-26"

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
- Make sure that IBM Knowledge Catalog and {{site.data.keyword.lakehouse_short}} are configured with [service-to-service authorization](watsonxdata?topic=watsonxdata-s2s_auth) in {{site.data.keyword.Bluemix_notm}}.
- Both {{site.data.keyword.lakehouse_short}} and IKC must be present in the {{site.data.keyword.Bluemix_notm}} environment.



## Connect and import the table metadata from {{site.data.keyword.lakehouse_short}} to IKC
{: #connect_import}
{: step}

1. Log in to [{{site.data.keyword.Bluemix_notm}}](https://cloud.ibm.com/).
1. Go to **Resource list** > **AI / Machine Learning** > **IBM Knowledge Catalog**.
1. Click **Launch in IBM Cloud Pak for Data**. The IBM Knowledge Catalog home page opens.

   A pop-up window opens with the options to create new catalog and category. If you prefer not to create them now, you can close the window.
   {: note}

1. From the left pane, go to **Catalogs** > **View all catalogs**. The **Catalogs** page opens with the list of available catalogs.
1. To create a new catalog:
    1. Click **New catalog**.
    1. On the **New catalog** page:
        - In the **Name** field, add a name for the catalog.
        - In the **Description** field, add a description.
        - From the **Object storage instance** drop-down list, select an object storage. If you don't have one, create an instance by clicking the link in the UI.
        - Select the **Enforce data protection and data location rules** checkbox to automatically enforce data protection and data location rules when you attempt to access data assets in the catalog.
        - Toggle the **Controls** switch to on poistion to allow reporting on asset metadata.
        - Choose an option to handle duplicate assets from the **Duplicate asset handling** section.
    1. Click **Create**. The catalog is created and the catalog page opens.
1. Go to **Add to catalog** > **Connection**.
1. On the **New connection** page, search and select {{site.data.keyword.lakehouse_full}}.
1. Enter the following details:
   | Field | Description |
   |-------|-------------|
   | Name | Enter the name of the connection. |
   | Description | Enter a connection description. |
   |Connect to IBM watsonx.data on Cloud Pak for Data| Do not select the checkbox. |
   | Hostname or IP address | Enter the {{site.data.keyword.lakehouse_short}} instance URL. For more information about retrieving the Hostname, see [Getting connection information](watsonxdata?topic=watsonxdata-get_connection). |
   | Port | Enter the port number. For more information about retrieving the Port, see [Getting connection information](watsonxdata?topic=watsonxdata-get_connection). |
   | Instance ID | Enter the instance ID. You can get the instance ID from the {{site.data.keyword.lakehouse_short}} instance home page (information icon). |
   | Instance name | Enter the {{site.data.keyword.lakehouse_short}} instance name. |
   | CRN | Enter the Cloud Resource Name. You can get the CRN from the {{site.data.keyword.lakehouse_short}} instance home page (information icon). |
   | Username | Enter your username (`ibmlhapikey_<EMAIL_ID>`). |
   | Password | Enter your IAM API key. To create one, see [Creating an API key](https://cloud.ibm.com/docs/account?topic=account-userapikey&interface=ui#create_user_key). |
   | SSL is enabled | Select the checkbox. |
   | SSL Certificate | Download the certificate from the watsonx.data console by using a web browser and paste in this field. |
   | Engine's hostname or IP address | Enter the engine hostname available in the {{site.data.keyword.lakehouse_short}} console without port number and `:`. |
   | Engine ID | Enter the engine ID available in the {{site.data.keyword.lakehouse_short}} console. |
   | Engine's port | Enter the engine port number available with the engine host name. |
   {: caption="Table 1. New connection" caption-side="bottom"}

1. Optional: Click **Test connection** to test the connection.
1. Click **Create**. The connection is added to the catalog.
1. Go to **Add to catalog** > **Connected assets**.
1. In the connected asset, click **Select source** and navigate to the table you want to import.
1. Select the table and click **Add**. The table asset is successfully added to IKC.

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
   | Service | Select **IBM Knowledge Catalog**. |
   | Storage catalogs | Select the applicable storage catalogs for IKC governance. |
   | IKC endpoint  | Configure the IKC API url. |
   {: caption="Table 1. Ingrate service" caption-side="bottom"}

1. Click **Integrate**.

## Verify the masking functionality as per the rules in IKC
{: #verify_mask}
{: step}

1. Login to IBM Knowledge Catalog.
1. From the left pane, go to **Governance** > **Rules**.
1. From the **Rules** page, verify that the rules corresponding to your data class of the column is defined. You can define a new rule by using **Add rule** button.

The owner can see the unmasked data. To verify whether masking is functioning correctly, log in to {{site.data.keyword.lakehouse_short}} as user who is not the owner of the asset in IKC and query the asset.
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
