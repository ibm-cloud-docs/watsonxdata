---

copyright:
  years: 2022, 2024
lastupdated: "2024-09-24"

keywords: lakehouse, watsonx.data, spark, cli

subcollection: watsonxdata

---

{{site.data.keyword.attribute-definition-list}}

# dbt Configuration (setting up your dbt profile)
{: #dbt_watsonx_spark_conf}

To connect dbt Core to your Spark engine, configure the `profiles.yml` file that is located in `.dbt` of your home directory.

The following is an example configuration:

```bash
{
  "api_key": "<add-your-apikey-here>",
  "crn": "<watsonx.data_instance_crn>",
  "environment_type": "SaaS",
  "host": "host IP address",
  "user_name": "<your_emailid>"
}
```
{: codeblock}

The following table covers the parameter details:

* **`<add-your-apikey-here>`** : Provide the API key. To generate the API key, see [Managing user API keys](https://cloud.ibm.com/docs/account?topic=account-userapikey&interface=ui#manage-user-keys).
* **host IP address** : Provide the host IP address of the watsonx.data install. To retrieve the host IP address, see [Getting connection information](watsonxdata?topic=watsonxdata-get_connection).
* **`<watsonx.data_instance_crn>`** : The **Instance CRN** of your watsonx.data instance. To retrieve the CRN, see [Getting connection information](watsonxdata?topic=watsonxdata-get_connection).
* **`<your_emailid>`** : Your email-id if you are using your API key or it should be in the format `<Service-id>-<GUID>`. For more information on generating service id and GUID, see [Creating service IDs](https://www.ibm.com/docs/en/watsonx/watsonxdata/aws?topic=2u-granting-access-through-service-ids-api-keys-from-saas-console#creating_service_IDs).
