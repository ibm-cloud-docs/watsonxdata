---

copyright:
  years: 2022, 2024
lastupdated: "2024-08-02"

keywords: watsonxdata, qhmm

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

# Query monitoring
{: #qhmm}

Query History Monitoring and Management (QHMM) is a service that stores and manages diagnostic data, such as query history and query event-related information of the Presto engine (Presto) in the default Minio bucket, wxd-system. You can retrieve the history files to analyze, debug or monitor the queries. You can also store the data in your own bucket.
{: shortdesc}

## Procedure
{: #prc_qhmm}

1. Log in to the {{site.data.keyword.lakehouse_short}} console.
2. From the navigation menu, select **Configurations**.
3. Click **Query monitoring**. The **Query monitoring** page opens.
4. You can view the QHMM configuration details. The following details are available:
    * Status of QHMM - Enabled or disabled.
    * Bucket that is configured to store QHMM data.
    * The subpath in the bucket where QHMM data is available.
5. To edit the configuration details, click **Edit** and make the required changes. You can enable or disable query monitoring, , and change the bucket.
6. Click **Save** after making the changes.
