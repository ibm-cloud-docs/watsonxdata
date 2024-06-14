---

copyright:
  years: 2022, 2024
lastupdated: "2024-05-31"

keywords: watsonx.data, spark, analytics, configuring
subcollection: watsonxdata

---

{{site.data.keyword.attribute-definition-list}}

# Retrieving parameter values
{: #ret_credentials}

The following table describe the parameters required to configure the Milvus details in watsonx.ai.




| Parameter | Retrieval procedure |
|--------------------------|----------------|
| PROJECT ID | 1. Go to [IBM watsonx home page](https://dataplatform.cloud.ibm.com/wx/home?context=wx). \n 2. From the navigation menu, select **Projects** > **View all projects** .\n 1. Click on your project. The project window opens. \n 3. Go to **General** > **Manage** tab. \n 4. Copy the project ID from the **Project ID** field.|
| ACCESS_TOKEN | 1. Go to [IBM watsonx home page](https://dataplatform.cloud.ibm.com/wx/home?context=wx). \n 2. From the navigation menu, select **Projects** > **View all projects**. \n 1. Click on your project. The project window opens. \n 5. Go to **Access control** > **Access tokens** tab. \n 6. Click **New access token**. \n 1. Specify a name,  select an access role for the token, and click **Create**. Copy the `ACCESS_TOKEN`.|
| IBM_CLOUD_URL | 1. Open your watsonx.data instance. \n 2. From the URL, copy `https://<host_name>`. |
| API_KEY | 1. From the [IBM Cloud console](https://cloud.ibm.com/), go to **Manage > Access (IAM)**, and select the **API keys**. \n 2. Click **Create** to create an API key. \n 1. Copy the API key. |
| MILVUS_HOST | 1. Log in to the {{site.data.keyword.lakehouse_short}} console. \n 2. From the navigation menu, select **Infrastructure manager**. \n 3. Select the Milvus service. \n 3. Go to the **Details** tab. \n 4. Copy the host from the **GRPC host** field.  \n While pasting the host name, remove `grpc://` and the five digit port number from the host. For example: If the GRPC host is `grpc://xxx.xxx.lakehouse.dev.appdomain.cloud.xxxxx`, consider only: `xxx.xxx.lakehouse.dev.appdomain.cloud`.|
| MILVUS_PORT| 1. Log in to the {{site.data.keyword.lakehouse_short}} console. \n 2. From the navigation menu, select **Infrastructure manager**. \n 3. Select the Milvus service. \n 3. Click **Details** tab. \n 4. Copy the port number from the **GRPC host** field (numerical value at the end of host). |
| MILVUS_USER| The default value is `ibmlhapikey`.|
| MILVUS_PASSWORD|The password is the IBM Cloud API_KEY that you have generated. |
{: caption="Table 1. Parameter values " caption-side="bottom"}
