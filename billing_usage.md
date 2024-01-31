---

copyright:
  years: 2022, 2024
lastupdated: "2024-01-31"

keywords: lakehouse, watsonx data, roles, access
subcollection: watsonxdata

---

{:javascript: #javascript .ph data-hd-programlang='javascript'}
{:java: #java .ph data-hd-programlang='java'}
{:ruby: #ruby .ph data-hd-programlang='ruby'}
{:php: #php .ph data-hd-programlang='php'}
{:python: #python .ph data-hd-programlang='python'}
{:external: target="_blank" .external}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:tip: .tip}
{:important: .important}
{:note: .note}
{:deprecated: .deprecated}
{:pre: .pre}
{:video: .video}

# Billing and usage
{: #manage_bill}

Billing in {{site.data.keyword.lakehouse_full}} is based on the charge metrics defined by {{site.data.keyword.Bluemix_short}} service.
{: shortdesc}

The following charge matrices apply to {{site.data.keyword.lakehouse_short}}:

* Resource Unit (RU): A measure of resources managed, processed, or related to the use of {{site.data.keyword.lakehouse_short}} service instance. Here, compute and support services are considered resources.

* Compute cluster: Consists of coordinator and worker nodes that run the query engine. Each node consumes a set of resource units per hour (as defined by the {{site.data.keyword.Bluemix_short}}) until the node is paused or deleted.

* Support services: Consists of supporting services such as metadata storage and access control.

The resource unit consumption begins after you provision the support services. The RUs are consumed on a per-hour basis and continue until you delete the instance.

You can view the estimate of the expected per hour run rate consumption of **Resource Units** from the **About** tab in the [**{{site.data.keyword.lakehouse_short}}** **{{site.data.keyword.Bluemix_short}} catalog**](https://cloud.ibm.com/watsonxdata) page.

The **Billing and Usage** page provides the latest information about RU consumption breakdown of the instance (based on the resource utilization).

To view current billing and usage details, complete the following steps:

1. Log in to the {{site.data.keyword.lakehouse_short}} console.

1. From the navigation menu, select **Billing and usage**. The **Billing and usage** page opens.

    The **Total run rate** field displays the sum of the run rates of all currently running infrastructure components in the instance.

    The billable infrastructure components are listed in the table. You can also type the component name in the **Search** field to list a particular component.

To customize the table display, click the **Customize columns** icon to select the columns to display.
{: note}

To manage the billing and usage functions from IBM Cloud, click **Manage in IBM Cloud** link. The [IBM Cloud Billing and usage](https://cloud.ibm.com/billing) page appear.
{: note}

The following are the fields in the **Billing and usage** page:

| Field           | Description        |
|------------------|--------------------|
| Display name     | The name of the billable component. |
| Status      | The status of the component. It can be running, failed, provisioning, restarting, resuming, scaling, updating, or paused. The **Running** status displays a run rate above 0 RUs/hour. |
| Component type            | The category of the component. |
| Run rate             | The resource units that are consumed per hour. |
{: caption="Table 1. Billing and usage" caption-side="bottom"}
