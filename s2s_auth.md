---

copyright:
  years: 2022, 2025
lastupdated: "2025-12-09"

keywords: watsonx.data, ikc, configuring, intelligence
subcollection: watsonxdata

---

{{site.data.keyword.attribute-definition-list}}

# Service to service authorization
{: #s2s_auth}

For integrating {{site.data.keyword.lakehouse_full}} with IBM watsonx.data intelligence, you must configure service-to-service authorization in {{site.data.keyword.Bluemix_notm}}.
A service authorization grants a source service or group of services in any account access to a target service or group of services in this account. You must be in the account where the target service is deployed.

Ensure that the required steps are first completed in the watsonx.data account and then repeated in the watsonx.data intelligence account, logging in separately to each environment.

## Procedure
{: #s2s_auth_procedure}

1. Log in to [{{site.data.keyword.Bluemix_notm}}](https://cloud.ibm.com/) where watsonx.data is deployed.
1. Go to **Manage** > **Access (IAM)**. The **IBM Cloud Identity and Access Management** page opens.
1. From the left panel, select **Authorizations**.
1. On the **Manage authorizations** page, click **Create**.
1. On the **Grant a service authorization** page:
   - If you are setting up authorization in your account, select **This account**.
   - If you are setting up authorization in the enterprise account, select **Other account**.
1. Search and select IBM watsonx.data intelligence as the source and {{site.data.keyword.lakehouse_short}} as the target.
1. Select **All resources** as the scope of access.
1. Select all the three roles:
   - **Viewer**
   - **DataAccess**
   - **MetastoreViewer**
1. Click **Authorize**.
1. Log in to the account where watsonx.data intelligence (IKC) is deployed.
1. On the **Manage authorizations** page, click **Create**.
1. Repeat steps 5 to 7 by selecting {{site.data.keyword.lakehouse_short}} as the source and IBM watsonx.data intelligence as the target.
1. Select the **Watsonx.data Service Access** role and click **Authorize**.


If you skip these steps, you may still be able to test the connection and add data from it, but metadata enrichment will fail and produce the following error:

``` bash
Failed to get Flight info: CDICO0100E: Connection failed: SQL error: Client error: Authentication failed: Unauthorized
```
{: codeblock}
