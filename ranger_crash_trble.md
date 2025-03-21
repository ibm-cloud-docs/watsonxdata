---

copyright:
  years: 2017, 2025
lastupdated: "2025-03-21"

keywords: watsonx.data, spark, analytics, provisioning
subcollection: watsonxdata

---

{{site.data.keyword.attribute-definition-list}}


# Why do I receive an error while integrating with Ranger?
{: #ts-ranger}
{: troubleshoot}

When you try to establish a connection with Ranger server, "Ranger is currently unavailable. Using cached configuration data temporarily until it expires. Restore Ranger to continue the service" is displayed.
{: tsSymptoms}


The `Policy Cache Time Configuration` defined in the watsonx.data `Integrations` page is more.
{: tsCauses}

To resolve this, you can verify the following.
{: tsResolve}


1. Verify the Apache Ranger details configured in the watsonx.data **Integrations** page.
2. Monitor the **Policy Cache Time Configuration** defined in the watsonx.data **Integrations** page. This setting specifies the time taken to refresh the newly defined Ranger policies.

If no value is specified, the default value of 10 minutes applies.
