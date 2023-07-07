---

copyright:
  years: 2022, 2023
lastupdated: "2023-07-07"

keywords: watsonx.data, update

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

# Presto update process for {{site.data.keyword.lakehouse_short}}
{: #update-wxd}

{{site.data.keyword.lakehouse_full}} is a managed service with regular release updates occurring as part of standard operations.
{: shortdesc}

<!-- After a new version becomes available, you receive an email notification. This email informs you about the new version and the start date of the update scheduling process. Starting from this day, you can expect your service version to be updated. -->


The upgrade process is designed to ensure that any outage is kept to a minimum. Your applications must be designed to handle temporary interruptions to the service by implementing the following:

* error handling for failed commands
* retry logic to recover from a temporary interruption

<!-- Following are some of the error codes that you might encounter during the update procedure: -->



<!-- Pending on the error code list from engine team -->

If a Presto coordinator node restarts on update, applications must re-establish connection with the Presto engine.

Before updates begin and after the new version becomes available, the latest version can be tested. A new presto engine can be provisioned from the infrastructure manager within your {{site.data.keyword.lakehouse_short}} instance, which uses the latest version thereby ensuring that all applications work seamlessly with the new version.

Applications can then be migrated to the new engine at your convenience, allowing better control of the update.
For more information, see [Creating an engine](watsonxdata?topic=watsonxdata-prov_engine).
