---

copyright:
  years: 2017, 2024
lastupdated: "2024-12-28"

keywords: watsonx.data, spark, analytics, provisioning
subcollection: watsonxdata

---

{{site.data.keyword.attribute-definition-list}}

# View and manage applications
{: #mng_appltn}

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

## Related API
{: #managespark_api}

For information on related API, see
* [List all applications in a spark engine](https://cloud.ibm.com/apidocs/watsonxdata#list-spark-engine-applications)
* [Submit engine applications](https://cloud.ibm.com/apidocs/watsonxdata#create-spark-engine-application)
* [Stop spark applications](https://cloud.ibm.com/apidocs/watsonxdata#delete-spark-engine-applications)
* [Get spark application](https://cloud.ibm.com/apidocs/watsonxdata#get-spark-engine-application-status)
