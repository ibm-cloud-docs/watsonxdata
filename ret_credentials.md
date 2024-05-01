---

copyright:
  years: 2022, 2024
lastupdated: "2024-04-30"

keywords: watsonx.data, spark, analytics, configuring
subcollection: watsonxdata

---

{{site.data.keyword.attribute-definition-list}}

# Configuring Environment file
{: #ret_credentials}

To establish connection with Milvus, configure the following Environment file.


   ```bash
   PROJECT_ID=<INSERT_PROJECT_ID>
   ACCESS_TOKEN=<INSERT_PROJECT_TOKEN>
   IBM_CLOUD_URL=<ibm_cloud_url>
   API_KEY= <api_key>

   MILVUS_HOST=<MILVUS_HOST>
   MILVUS_PORT=<MILVUS_PORT>
   MILVUS_USER=ibmlhadmin
   MILVUS_PASSWORD=<MILVUS_PASSWORD>
   ```
   {: codeblock}

Furnish the following parameters.


| Parameter | Retrieval procedure |
|--------------------------|----------------|
| PROJECT ID | 1. Go to [IBM watsonx home page](https://dataplatform.cloud.ibm.com/wx/home?context=wx). \n 2. From the navigation menu, select **Projects** > **View all projects** .\n 1. Click on your project. The project window opens. \n 3. Go to **General** > **Manage** tab. \n 4. Copy and paste the project ID from the **Project ID** field into your `confi.env` file.|
| ACCESS_TOKEN | 1. Go to [IBM watsonx home page](https://dataplatform.cloud.ibm.com/wx/home?context=wx). \n 2. From the navigation menu, select **Projects** > **View all projects**. \n 1. Click on your project. The project window opens. \n 5. Go to **Access control** > **Access tokens** tab. \n 6. Click **New access token**. \n 1. Specify a name,  select an access role for the token, and click **Create**. Copy and paste the `ACCESS_TOKEN` into your `confi.env` file.|
| IBM_CLOUD_URL | 1. Open your watsonx.data instance. \n 2. From the URL, copy `https://<host_name>` into your `confi.env` file. |
| API_KEY | 1. From the [IBM Cloud console](https://cloud.ibm.com/), go to **Manage > Access (IAM)**, and select the **API keys**. \n 2. Click **Create** to create an API key. \n 1. Copy and paste the API key into your `confi.env` file. |
| MILVUS_HOST | 1. Log in to the {{site.data.keyword.lakehouse_short}} console. \n 2. From the navigation menu, select **Infrastructure manager**. \n 3. Select the Milvus service. \n 3. Go to the **Details** tab. \n 4. Copy and paste the host from the **Host** field into your `confi.env` file. For example, `xxx.xxx.lakehouse.dev.appdomain.cloud`.|
| MILVUS_PORT| 1. Log in to the {{site.data.keyword.lakehouse_short}} console. \n 2. From the navigation menu, select **Infrastructure manager**. \n 3. Select the Milvus service. \n 3. Click **Details** tab. \n 4. Copy the port number from the **Host** field (numerical value at the end of host). |
| MILVUS_USER| The default value is `ibmlhapikey`.|
| MILVUS_PASSWORD|The password is the IBM Cloud API_KEY that you have generated. |
{: caption="Table 1. Parameter values " caption-side="bottom"}
