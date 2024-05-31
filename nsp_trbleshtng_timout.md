---

copyright:
  years: 2017, 2024
lastupdated: "2024-05-31"

keywords: watsonx.data, spark, analytics, provisioning
subcollection: watsonxdata

---

{{site.data.keyword.attribute-definition-list}}


# Why do I receive a timeout error while connecting to Spark labs?
{: #ts-nsp-time}
{: troubleshoot}

You fail to connect to Spark labs because of a timed-out connection to the host or the connection automatically drops after a few seconds.
{: tsSymptoms}


Update the following settings from Visual Studio Code.
{: tsResolve}


1. Open **Settings** from **Visual Studio Code**.
2. Search for **Use Exec Server** and select the checkbox to enable the feature.
3. Refresh Spark labs extension by clicking the **Refresh** icon from the left navigation pane and try reconnecting.
