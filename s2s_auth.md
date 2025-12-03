---

copyright:
  years: 2022, 2025
lastupdated: "2025-12-03"

keywords: watsonx.data, ikc, configuring, knowledgecatalog
subcollection: watsonxdata

---

{{site.data.keyword.attribute-definition-list}}

# Service to service authorization
{: #s2s_auth}

For integrating {{site.data.keyword.lakehouse_full}} with IBM watsonx.data intelligence, you must configure service-to-service authorization in {{site.data.keyword.Bluemix_notm}}.
A service authorization grants a source service or group of services in any account access to a target service or group of services in this account. You must be in the account where the target service is deployed.

## Procedure
{: #s2s_auth_procedure}

1. Log in to [{{site.data.keyword.Bluemix_notm}}](https://cloud.ibm.com/). Log in to the account where watsonx.data is deployed.
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
1. Repeat steps 5 to 7 by selecting {{site.data.keyword.lakehouse_short}} as the source and IBM Knowledge Catalog as the target.
1. Select the **Watsonx.data Service Access** role and click **Authorize**.


If you skip these steps, you may still be able to test the connection and add data from it, but metadata enrichment will fail and produce the following error:

``` bash
Asset failures: 12 2025-11-10T21:25:48.011Z - 82d7276a-9570-4c11-85c7-bd4374375d69 [PROF] (HB task id: 28b002d7-0221-40b5-a577-2a8ff7bc5df9, HB job id: 42471afc-6710-4fec-86fe-5c7ef3fc1d15) ("customer") - Failed to get Flight info: CDICO0100E: Connection failed: SQL error: Client error: Authentication failed: Unauthorized 2025-11-10T21:25:50.849Z - a88a9c14-4881-4a96-9a22-85f1f0d0a6f1 [PROF] (HB task id: 28b002d7-0221-40b5-a577-2a8ff7bc5df9, HB job id: 42471afc-6710-4fec-86fe-5c7ef3fc1d15) ("agent") - Failed to get Flight info: CDICO0100E: Connection failed: SQL error: Client error: Authentication failed: Unauthorized 2025-11-10T21:25:51.294Z - 5a8a5592-f1d1-44c4-94a6-43647e58c5dd [PROF] (HB task id: 28b002d7-0221-40b5-a577-2a8ff7bc5df9, HB job id: 42471afc-6710-4fec-86fe-5c7ef3fc1d15) ("schedule_lookup") - Failed to get Flight info: CDICO0100E: Connection failed: SQL error: Client error: Authentication failed: Unauthorized 2025-11-10T21:25:52.105Z - 6bdefc47-0040-41d4-a4e3-1a29ef7ecbb9 [PROF] (HB task id: 28b002d7-0221-40b5-a577-2a8ff7bc5df9, HB job id: 42471afc-6710-4fec-86fe-5c7ef3fc1d15) ("call_center_site_location") - Failed to get Flight info: CDICO0100E: Connection failed: SQL error: Client error: Authentication failed: Unauthorized 2025-11-10T21:25:59.849Z - 2ab690ce-0031-45a1-a724-9192e5041e85 [PROF] (HB task id: 28b002d7-0221-40b5-a577-2a8ff7bc5df9, HB job id: 42471afc-6710-4fec-86fe-5c7ef3fc1d15) ("summary") - Failed to get Flight info: CDICO0100E: Connection failed: SQL error: Client error: Authentication failed: Unauthorized 2025-11-10T21:26:05.481Z - 05cf5c52-d05c-416f-b5c9-950b514148ca [PROF] (HB task id: 28b002d7-0221-40b5-a577-2a8ff7bc5df9, HB job id: 42471afc-6710-4fec-86fe-5c7ef3fc1d15) ("call_type_lookup") - Failed to get Flight info: CDICO0100E: Connection failed: SQL error: Client error: Authentication failed: Unauthorized 2025-11-10T21:26:05.574Z - 2dc35e54-a8a6-48f4-941e-8276beaa0a32 [PROF] (HB task id: 28b002d7-0221-40b5-a577-2a8ff7bc5df9, HB job id: 42471afc-6710-4fec-86fe-5c7ef3fc1d15) ("summary_mv") - Failed to get Flight info: CDICO0100E: Connection failed: SQL error: Client error: Authentication failed: Unauthorized 2025-11-10T21:26:06.361Z - 8c47f3a8-c745-4900-9152-d2166f8f0f35 [PROF] (HB task id: 28b002d7-0221-40b5-a577-2a8ff7bc5df9, HB job id: 42471afc-6710-4fec-86fe-5c7ef3fc1d15) ("phone_plan") - Failed to get Flight info: CDICO0100E: Connection failed: SQL error: Client error: Authentication failed: Unauthorized 2025-11-10T21:26:17.731Z - 830875ea-7622-4a9c-847d-52ad887cbcbe [PROF] (HB task id: 28b002d7-0221-40b5-a577-2a8ff7bc5df9, HB job id: 42471afc-6710-4fec-86fe-5c7ef3fc1d15) ("call_resolution_lookup") - Failed to get Flight info: CDICO0100E: Connection failed: SQL error: Client error: Authentication failed: Unauthorized 2025-11-10T21:26:28.414Z - 06925db0-4334-4210-a38e-cb5fe392ee72 [PROF] (HB task id: 28b002d7-0221-40b5-a577-2a8ff7bc5df9, HB job id: 42471afc-6710-4fec-86fe-5c7ef3fc1d15) ("call_log_fact") - Failed to get Flight info: CDICO0100E: Connection failed: SQL error: Client error: Authentication failed: Unauthorized 2025-11-10T21:26:30.245Z - 873f6f56-afc1-4b5c-a07c-209780ebbdc6 [PROF] (HB task id: 28b002d7-0221-40b5-a577-2a8ff7bc5df9, HB job id: 42471afc-6710-4fec-86fe-5c7ef3fc1d15) ("supervisor") - Failed to get Flight info: CDICO0100E: Connection failed: SQL error: Client error: Authentication failed: Unauthorized 2025-11-10T21:26:33.314Z - ba2e9af5-b533-4d29-b5d8-be3ce648ce48 [PROF] (HB task id: 28b002d7-0221-40b5-a577-2a8ff7bc5df9, HB job id: 42471afc-6710-4fec-86fe-5c7ef3fc1d15) ("shift_lookup") - Failed to get Flight info: CDICO0100E: Connection failed: SQL error: Client error: Authentication failed: Unauthorized

```
{: codeblock}
