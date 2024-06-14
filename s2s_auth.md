---

copyright:
  years: 2022, 2024
lastupdated: "2024-06-13"

keywords: watsonx.data, ikc, configuring, knowledgecatalog
subcollection: watsonxdata

---

{{site.data.keyword.attribute-definition-list}}

# Service to service Authorization
{: #s2s_auth}

For integrating {{site.data.keyword.lakehouse_full}} with IBM Knowledge Catalog (IKC), you must configure service-to-service authorization in {{site.data.keyword.Bluemix_notm}}.

## Procedure
{: #s2s_auth_procedure}

1. Log in to [{{site.data.keyword.Bluemix_notm}}](https://cloud.ibm.com/).
1. Go to **Manage** > **Access (IAM)**. The **IBM Cloud Identity and Access Management** page opens.
1. From the left panel, select **Authorizations**.
1. On the **Manage authorizations** page, click **Create**.
1. On the **Grant a service authorization** page:
   - If you are setting up authorization in your account, select **This account**.
   - If you are setting up authorization in the enterprise account, select **Other account**.
1. Search and select IBM Knowledge Catalog as the source and {{site.data.keyword.lakehouse_short}} as the target.
1. Select all of the three roles:
   - **Viewer**
   - **DataAccess**
   - **MetastoreViewer**
1. Click **Authorize**.
1. On the **Manage authorizations** page, click **Create**.
1. Do the steps 5 and 6 by selecting {{site.data.keyword.lakehouse_short}} as the source and IBM Knowledge Catalog as the target.
1. Select the **Watsonx.data Service Access** role and click **Authorize**.
