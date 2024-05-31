---

copyright:
  years: 2017, 2024
lastupdated: "2024-05-31"

keywords: watsonx.data, spark, analytics, provisioning
subcollection: watsonxdata

---

{{site.data.keyword.attribute-definition-list}}


# Why do I receive a certificate error while connecting to Spark labs?
{: #ts-nsp-cert}
{: troubleshoot}

When you try to establish a connection with Spark labs, "Certificate error" is displayed.
{: tsSymptoms}


Your watsonx.data endpoint does not have a secure SSL certificate that is installed in the machine.
{: tsCauses}

To resolve this, you can configure the settings to disable SSL verification.
{: tsResolve}


1. Open **Settings** from **Visual Studio Code**.
2. Search for **Verify SSL** and disble the feature.
3. Refresh Spark labs extension by clicking the **Refresh** icon from the left navigation pane and try reconnecting.
