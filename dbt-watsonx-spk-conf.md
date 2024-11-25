---

copyright:
  years: 2022, 2024
lastupdated: "2024-11-25"

keywords: lakehouse, watsonx.data, spark, cli

subcollection: watsonxdata

---

{{site.data.keyword.attribute-definition-list}}

# dbt Configuration (setting up your dbt profile)
{: #dbt_watsonx_spark_conf}

To connect dbt core to your Spark engine, configure the `profiles.yml` file that is located in `.dbt` of your home directory.

The following is an example configuration:

```bash
profile_name:
  target: "dev"
  outputs:
    dev:
      type: "watsonx_spark"
      method: "http"
      schema: "<wxd-schema>"
      host: "https://us-south.lakehouse.cloud.ibm.com"
      uri: "/lakehouse/api/v2/spark_engines/spark216/query_servers/02bda638-1399-4914-8ae7-ab4223764d26/connect/cliservice"
      catalog: "<wxd-catalog>"
      auth:
        instance: "<watsonx.data_instance_crn>"
        user: "<username>"
        apikey: "<apikey>"

```
{: codeblock}

The following list covers the parameter details:

* **profile_name**: The profile name as the dbt project name.

* **schema**: The table schema name associated with the Spark engine's catalog.

   If the specified schema does not exist in the chosen catalog, a new schema is created automatically. If you want to create a new schema in your storage, add `location_root` with the value `s3a://{your_bukect_name}/{your_schema_name}`.
   {: note}

* **host**: Hostname of your {{site.data.keyword.lakehouse_short}} console. For more information, see [Getting connection information]({{site.data.keyword.ref-get_connection-link}}).

* **uri**:  URI of your query server that is running on {{site.data.keyword.lakehouse_short}}. For more information, see [Getting connection information]({{site.data.keyword.ref-get_connection-link}}).

* **catalog**: The catalog that is associated with the Spark engine.

* **instance**: The instance CRN of your {{site.data.keyword.lakehouse_short}} instance. To retrieve the CRN, see [Getting connection information]({{site.data.keyword.ref-get_connection-link}}).

* **user**: Your email-id if you are using your API key or it should be in the format `<Service-id>-<GUID>`. For more information on generating service id and GUID, see [Creating service IDs](https://www.ibm.com/docs/en/watsonx/watsonxdata/aws?topic=usca-granting-access-through-service-ids-api-keys-from-saas-console#creating_service_IDs).

* **apikey**: Your API key. To generate the API key, see [Managing user API keys](https://cloud.ibm.com/docs/account?topic=account-userapikey&interface=ui#manage-user-keys).
