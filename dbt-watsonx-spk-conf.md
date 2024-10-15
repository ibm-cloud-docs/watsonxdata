---

copyright:
  years: 2022, 2024
lastupdated: "2024-10-15"

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
      host: "https://us-south.lakehouse.dev.cloud.ibm.com"
      uri: "/lakehouse/api/v2/spark_engines/spark216/query_servers/02bda638-1399-4914-8ae7-ab4223764d26/connect/cliservice"
      auth:
        instance: "<watsonx.data_instance_crn>"
        user: "<username>"
        apikey: "<apikey>"
      location_root: "s3a://<bucket-name>/<wxd-schema>"
```
{: codeblock}

The following table covers the parameter details:

* **profile_name** : Provide the profile name as the dbt project name.
* **`<wxd-schema>`** : The table schema name that is associated with the Spark engine that you need to run the dbt models.
* **host IP address** : Provide the host IP address of the watsonx.data install. To retrieve the host IP address, see [Getting connection information](watsonxdata?topic=watsonxdata-get_connection).
* **`<watsonx.data_instance_crn>`** : The **Instance CRN** of your watsonx.data instance. To retrieve the CRN, see [Getting connection information](watsonxdata?topic=watsonxdata-get_connection).
* **`<username>`** : Your email-id if you are using your API key or it should be in the format `<Service-id>-<GUID>`. For more information on generating service id and GUID, see [Creating service IDs](https://www.ibm.com/docs/en/watsonx/watsonxdata/aws?topic=2u-granting-access-through-service-ids-api-keys-from-saas-console#creating_service_IDs).
* **`<<apikey>`** : Provide the API key. To generate the API key, see [Managing user API keys](https://cloud.ibm.com/docs/account?topic=account-userapikey&interface=ui#manage-user-keys).
* In case you want to create a new schema in your storage then add `location_root` with the value `s3a://{your_bukect_name}/{your_schema_name}`.
