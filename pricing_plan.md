---

copyright:
  years: 2022, 2024
lastupdated: "2024-08-23"

keywords: lakehouse, data types, connectors, watsonx.data

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

# {{site.data.keyword.lakehouse_full}} pricing plans
{: #pricing-plans-1}

{{site.data.keyword.lakehouse_full}} as a Service offers three plans.

## Lite plan
{: #lite-plan-1}

The Lite plan is provided for you to try the basic features of {{site.data.keyword.lakehouse_short}} and is available to all {{site.data.keyword.Bluemix_notm}} account types like trial, pay-as-you-go, and subscription. It supports the basic features only. It is not available on AWS and is limited to one {{site.data.keyword.lakehouse_short}} instance per {{site.data.keyword.Bluemix_notm}} account (cross-regional).

### Key supported features
{: #supported-features-lite}

- Ability to monitor Resource Unit usage across Lite plan instances per an account and provision a new Lite plan instance based on the Resource Unit availability.
- Ability to pause and resume Presto engine.
- Ability to provision, unprovision, pause and resume Spark engine.
- Ability to connect to an {{site.data.keyword.Bluemix_notm}}-provided Cloud Object Storage (COS) bucket and provide credentials to your own COS or S3 bucket.
- Ability to delete Presto, Spark, Milvus, and connections to your own bucket.

### Limitations
{: #limitations-lite}

- The Lite plan is limited to 2000 resource units (RUs) before the instance is suspended. The cap value is displayed on the [{{site.data.keyword.Bluemix_notm}} catalog provisioning][def] page and is reflected on your billing page within your {{site.data.keyword.lakehouse_short}} instance upon provisioning. Your plan expires on reaching either the cap limit of 2000 RUs or exceeding the trial period of 30 days.
- The Lite plan is limited to a maximum of one Presto engine, one Spark engine (small size, single node) or Milvus service with starter size (1.25 RUs per hour) or all three.
- The Lite plan is limited to the smallest node sizes and profiles for each engine and service. You cannot increase the node size.
- The Lite plan instances cannot be used for production purposes.
- The Lite plan might be removed anytime.
- The Lite instances are unrecoverable (no BCDR).
- Engine scaling functionality is not available in the Lite plan.
- Milvus back up is not available with the Lite plan.

You must be connected to your own bucket to save and backup any data that is external to the Lite instance before full consumption of the Lite plan resource units.
{: important}

To upgrade to another plan, you must have a pay-as-you-go or subscription {{site.data.keyword.Bluemix_notm}} account and provision a distinct Enterprise instance of {{site.data.keyword.lakehouse_short}}.
{: note}

## Enterprise plan
{: #enterprise-plan}

You must have a pay-as-you-go or subscription {{site.data.keyword.Bluemix_notm}} account to avail the Enterprise plan. It is available on {{site.data.keyword.Bluemix_notm}} and AWS environments. Presto engine and Milvus service are available with this plan.

### Key supported features
{: #supported-features-ep}

- Ability to scale (increase and decrease) node sizes for Presto engines.
- Ability pause and resume Presto engines.



[def]: https://cloud.ibm.com/watsonxdata
