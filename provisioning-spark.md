---

copyright:
  years: 2017, 2023
lastupdated: "2023-08-24"

keywords: watsonx.data, spark, analytics, provisioning
subcollection: watsonxdata

---

{{site.data.keyword.attribute-definition-list}}

# Provisioning an {{site.data.keyword.iae_short}} instance
{: #lh-provisioning-serverless}

For {{site.data.keyword.lakehouse_short}}, it is recommended to use {{site.data.keyword.iae_full_notm}} Spark to achieve below use-cases:
1. Ingesting large volumes of data into {{site.data.keyword.lakehouse_short}} tables. You can also cleanse and transform data before ingestion.
2. Table maintenance operation to enhance {{site.data.keyword.lakehouse_short}} performance of the table
3. Complex analytics workload which are difficult to represent as queries.



You can create an {{site.data.keyword.iae_full_notm}} instance:

- [Using the {{site.data.keyword.Bluemix_short}} console](#lh-console-provisioning)
- [Using the {{site.data.keyword.Bluemix_short}} command-line interface](#lh-cli-provisioning)
- [Using the Resource controller REST API](#lh-rest-api-provisioning)

You must have access to either the {{site.data.keyword.Bluemix_short}} us-south (Dallas) or the eu-de (Frankfurt) region. When you add a region for provisioning an {{site.data.keyword.iae_short}} instance, choose one that is closer to the region where you have provisioned {{site.data.keyword.lakehouse_short}} to avoid data latency issues.
{: important}

## Creating a service instance from the {{site.data.keyword.Bluemix_short}} console
{: #lh-console-provisioning}

You can create an instance by using the {{site.data.keyword.Bluemix_short}} console.


To create an {{site.data.keyword.iae_full_notm}} instance:
1. Log in to the [{{site.data.keyword.Bluemix_short}} console](https://{DomainName}/catalog){: external}.
1. Click **Services** and select the category **Analytics**.
1. Search for {{site.data.keyword.iae_short}} and then click the tile to open the service instance creation page.
1. Choose the location that is closer to the region where you have provisioned {{site.data.keyword.lakehouse_short}} for deploying the service instance. Currently, **us-south** and **eu-de** are the only supported regions.
1. Select a plan. Currently, **Standard Serverless for Apache Spark** is the only supported serverless plan.
1. Configure the instance by entering a name of your choice, selecting a resource group and adding tags.
1. Select latest runtime version available (for example 3.3).
1. Select the {{site.data.keyword.cloud_notm}} Object Storage instance from your account that you want to use as the {{site.data.keyword.iae_short}} **instance home** to store instance-related data.
1. Click **Create** to provision the service instance in the background.

    The newly created service is listed in your [{{site.data.keyword.Bluemix_short}} resource list](https://{DomainName}/resources){: external} under **Services**.

## Creating a service instance by using the {{site.data.keyword.Bluemix_short}} command-line interface
{: #lh-cli-provisioning}

To create a service instance by using the {{site.data.keyword.Bluemix_short}} command-line interface:


1. Download and configure the {{site.data.keyword.Bluemix_short}} CLI. Follow the instructions in [Getting started with the {{site.data.keyword.Bluemix_short}} CLI](/docs/cli?topic=cli-getting-started){: external}.

1. Set the API endpoint for your region and log in:
    ```bash
    ibmcloud api https://DOMAIN_NAME
    ibmcloud login
    ```
    {: codeblock}

    Parameter value:
    * DOMAIN_NAME: The API endpoint for your region. For example, cloud.ibm.com

1. Get the list of the resource groups for your account and select one of the returned resource groups as the target resource group in which to create the {{site.data.keyword.iae_full_notm}} serverless instance:
    ```bash
    ibmcloud resource groups
    ibmcloud target -g <RESOURCE_GROUP_NAME>
    ```
    {: codeblock}

    Parameter value:
    * RESOURCE_GROUP_NAME: Provide the same name as you specified while provisioning watsonx.data for efficient organizing.

1. Create a service instance:
    ```bash
    ibmcloud resource service-instance-create <SERVICE_INSTANCE_NAME> ibmanalyticsengine <PLAN_NAME> <REGION> -p @<PATH_to JSON file with cluster parameters>
    ```
    {: codeblock}

    Parameter value:
    * SERVICE_INSTANCE_NAME: Specify a name for the instance.
    * PLAN_NAME: Specify the plan name as **plan_name8afde05e-5fd8-4359-a597-946d8432dd45**.
    * REGION: Specify the region where you like to provision the instance.

    Note that currently, standard-serverless-spark is the only supported serverless plan and us-south and eu-de the only supported regions. Choose one that is closer to the region where you have provisioned watsonx.data.
    {: note}

    * PATH_to JSON file: Include the path to the JSON file that contains the provisioning parameters.

    For example, for the Dallas region:
    ```bash
    ibmcloud resource service-instance-create MyServiceInstance ibmanalyticsengine standard-serverless-spark us-south -p @provision.json
    ```
    {: codeblock}

    You can give the service instance any name you choose.
    Note that currently, **standard-serverless-spark** is the only supported serverless plan and **us-south** and **eu-de** the only supported regions.
    {: note}

    The `provision.json` file contains the provisioning parameters for the instance that you want to create.

    The endpoint to your {{site.data.keyword.Bluemix_short}} Object Storage instance in the payload JSON file must be the direct endpoint. Direct endpoints provide better performance than public endpoints and do not incur charges for any outgoing or incoming bandwidth.

    Following is a sample provision.json file.

    ```bash
    {
      "default_runtime": {
        "spark_version": "3.3"
        },
      "instance_home": {
        "region": "us-south",
        "endpoint": "https://s3.direct.us-south.cloud-object-storage.appdomain.cloud",
        "hmac_access_key": "<your-hmac-access-key",
        "hmac_secret_key": "<your-hmac-secret-key"
        },
      "default_config": {
        "key1": "value1",
        "key2": "value2"
        }
    }
    ```
    {: codeblock}

    The {{site.data.keyword.Bluemix_short}} response to the create instance command:
    ```text
    Creating service instance MyServiceInstance in resource group Default of account <your account name> as <your user name>...
    OK
    Service instance MyServiceInstance was created.

    Name:                MyServiceInstance
    ID:                  crn:v1:staging:public:ibmanalyticsengine:us-south:a/d628eae2cc7e4373bb0c9d2229f2ece5:1e32e***-afd9-483a-b1**-724ba5cf4***::
    GUID:                1e32e***-afd9-483a-b1**-724ba5cf4***
    Location:            us-south
    State:               provisioning
    Type:                service_instance
    Sub Type:
    Service Endpoints:   public
    Allow Cleanup:       false
    Locked:              false
    Created at:          2021-11-29T07:20:40Z
    Updated at:          2021-11-29T07:20:42Z
    Last Operation:
                        Status    create in progress
                        Message   Started create instance operation
    ```
    {: codeblock}

    The sample response to the create instance command is:
    ```bash
    Creating service instance MyServiceInstance in resource group Default of account <your account name> as <your user name>...
    OK
    Service instance MyServiceInstance was created.

    Name:                MyServiceInstance
    ID:                  crn:v1:staging:public:ibmanalyticsengine:us-south:a/d628eae2cc7e4373bb0c9d2229f2ece5:1e32e***-afd9-483a-b1**-724ba5cf4***::
    GUID:                1e32e***-afd9-483a-b1**-724ba5cf4***
    Location:            us-south
    State:               provisioning
    Type:                service_instance
    Sub Type:
    Service Endpoints:   public
    Allow Cleanup:       false
    Locked:              false
    Created at:          2021-11-29T07:20:40Z
    Updated at:          2021-11-29T07:20:42Z
    Last Operation:
                    Status    create in progress
                    Message   Started create instance operation
    ```
    {: codeblock}


    Make a note of the instance ID from the output. You will need the instance ID when you call instance management or Spark application management APIs. See [Spark application REST API](/docs/AnalyticsEngine?topic=AnalyticsEngine-spark-app-rest-api){: external}.
    {: important}

5. [Track instance readiness](#lh-instance-readiness).


## Creating a service instance by using the Resource controller REST API
{: #lh-rest-api-provisioning}

An {{site.data.keyword.iae_full_notm}} serverless instance must reside in an {{site.data.keyword.Bluemix_short}} resource group. As a first step toward creating an {{site.data.keyword.iae_full_notm}} serverless instance through the Resource controller REST API, you must have the resource group ID and serverless plan ID close at hand.

To create a service instance by using the Resource controller REST API:

1. Get the resource group ID by logging in to the {{site.data.keyword.Bluemix_short}} CLI and running the following command:
    ```bash
    ibmcloud resource groups
    ```
    {: codeblock}

    Sample result:
    ```bash
    Retrieving all resource groups under account <Account details..>
    OK
    Name      ID      Default Group   State
    Default   XXXXX   true            ACTIVE
    ```
1. Use the following resource plan ID for the Standard Serverless for Apache Spark plan:
    ```bash
    8afde05e-5fd8-4359-a597-946d8432dd45
    ```
    {: codeblock}

1. Get the IAM token. For instructions, see [steps](/docs/AnalyticsEngine?topic=AnalyticsEngine-retrieve-iam-token-serverless){: external}.
1. Create an instance by using the Resource controller REST API:
    ```bash
    curl -X POST https://resource-controller.cloud.ibm.com/v2/resource_instances/
    --header "Authorization: Bearer $token" -H 'Content-Type: application/json' -d @provision.json
    ```
    {: codeblock}

    The provision.json file contains the provisioning parameters for the instance that you want to create. See [Architecture and concepts in serverless instances](/docs/AnalyticsEngine?topic=AnalyticsEngine-serverless-architecture-concepts){: external} for a description of the provisioning parameters in the payload.


    Following is a sample of the `provision.json` file.
    ```bash
    {
      "name": "your-service-instance-name",
      "resource_plan_id": "8afde05e-5fd8-4359-a597-946d8432dd45",
      "resource_group": "resource-group-id",
      "target": "us-south",
      "parameters": {
        "default_runtime": {
          "spark_version": "3.3"
            },
            "instance_home": {
              "region": "us-south",
              "endpoint": "s3.direct.us-south.cloud-object-storage.appdomain.cloud",
              "hmac_access_key": "your-access-key",
              "hmac_secret_key": "your-secret-key"
              }
        }
    }
    ```
    {: codeblock}

1. [Track instance readiness](#lh-instance-readiness).

For more information on the Resource controller REST API for creating an instance, see [Create (provision) a new resource instance](/apidocs/resource-controller/resource-controller#create-resource-instance){: external}.

## Tracking instance readiness
{: #lh-instance-readiness}

To run applications on a newly created serverless instance, the instance must be in **active** state.


To track instance readiness:
1. Enter the following command:
    ```bash
    curl -X GET https://api.us-south.ae.cloud.ibm.com/v3/analytics_engines/{instance_id} -H "Authorization: Bearer $token"
    ```
    {: codeblock}

    Sample response:
    ```bash
    {
      "id": "dc0e****-eab2-4t9e-9441-56620949****",
      "state": "created",
      "state_change_time": "2021-04-21T04:24:01Z",
      "default_runtime": {
        "spark_version": "3.3",
        "instance_home": {
          "provider": "ibm-cos",
          "type": "objectstore",
          "region": "us-south",
          "endpoint": "https://s3.direct.us-south.cloud-object-storage.appdomain.cloud",
          "bucket": "ae-bucket-do-not-delete-dc0e****-eab2-4t**-9441-566209499546",
          "hmac_access_key": "eH****g=",
          "hmac_secret_key": "4d********76"
        },
        "default_config": {
          "spark.driver.memory": "4g",
          "spark.driver.cores": 1
        }
      }
    }
    ```
1. Check the value of the **state** attribute. It must be **active** before you can start running applications in the instance.

## Learn more
{: #lh-learnmore}

When provisioning serverless instances, follow the recommended [Best practices](/docs/AnalyticsEngine?topic=AnalyticsEngine-best-practices-serverless){: external}.
