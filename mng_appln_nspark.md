---

copyright:
  years: 2017, 2025
lastupdated: "2025-09-10"

keywords: watsonx.data, spark, analytics, provisioning
subcollection: watsonxdata

---

{{site.data.keyword.attribute-definition-list}}

# View and manage applications
{: #mng_appltn}


**Applies to** : [Spark engine]{: tag-blue}  [Gluten accelerated Spark engine]{: tag-green}


You can monitor the status of the applications that are submitted in the {{site.data.keyword.lakehouse_full}} instance.
Log in to the {{site.data.keyword.lakehouse_short}} cluster. Go to the Infrastructure manager page.

## View details of the submitted Spark applications in watsonx.data
{: #mng_appltn-1}


1. In the **Applications** tab, you can view the list of all applications that are submitted to {{site.data.keyword.lakehouse_short}}. The tab also displays the details such as the application status, Spark version, creation time, start time, and finish time.

Application status can be : ACCEPTED, FINISHED, FAILED, ERROR, RUNNING, SUBMITTED, STOPPED, or WAITING.
{: note}

2. Click the arrow to the left of an application ID in the result list, to view more details like **Spark application ID** and **Application name**.

You can also filter the applications based on status using the **Filter** icon.
{: note}

Track the status of the application by invoking the application status API, see [API](https://cloud.ibm.com/apidocs/watsonxdata#get-spark-engine-application-status).


## Stopping applications in {{site.data.keyword.lakehouse_short}}
{: #mng_appltn-2}

You can stop only the applications that are in RUNNING state.
{: important}

1. In the **Applications** tab, select the application that you want to stop.
1. Click the overflow menu and select **Stop**. The application status changes to `STOPPED`.



## Configure filter parameters to list Spark applications by using API
{: #mng_appl2}

You can use API, which allows to limit the number of Spark Applications listed. Also, you can filter applications by using additional filter options Application Name, Start Time Interval, and End Time Interval.


You can configure the following parameters and use the CURL command to add the filter parameters:

```bash
curl -k -X GET
https://<region>/lakehouse/api/<api_version>/spark_engines/<spark_engine_id>/applications?state=accepted,running,finished,failed&limit=<limit_value>&start_time_interval={start_lower timestamp limit},{start_upper timestamp limit}&end_time_interval={end_lower timestamp limit},{end_upper timestamp limit}
```
{: codeblock}


Parameter values:

* `<region>`: The region where the Spark instance is provisioned.

* `<spark_engine_id>` : The engine ID of the Spark engine.

* `<application_id>` : The application for which the details are viewed.

* `<limit_value>` : The instance ID from the watsonx.data cluster instance URL. For example, 1609968577169454.

* start_time_interval : Time interval to use for filtering applications by their start time. Specify {start_lower timestamp limit} and {start_upper timestamp limit} For example, 2025-04-08T00:00:00Z,2025-04-10T23:59:59Z.

* end_time_interval : Time interval to use for filtering applications by their end time. Interval is specified in the format. Specify {end_lower timestamp limit} and {end_upper timestamp limit} For example, 2024-04-08T00:00:00Z,2024-04-08T23:59:59Z.

* `<api_version>` :When using the v2 API, set the <api_version> parameter to `v2`; for the v3 API, set it to `v3`.



## Related API
{: #managespark_api}

For information on related API, see
* [List all applications in a spark engine](https://cloud.ibm.com/apidocs/watsonxdata#list-spark-engine-applications)
* [Submit engine applications](https://cloud.ibm.com/apidocs/watsonxdata#create-spark-engine-application)
* [Stop spark applications](https://cloud.ibm.com/apidocs/watsonxdata#delete-spark-engine-applications)
* [Get spark application](https://cloud.ibm.com/apidocs/watsonxdata#get-spark-engine-application-status)
