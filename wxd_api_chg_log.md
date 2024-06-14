---

copyright:
  years: 2022, 2024
lastupdated: "2024-05-31"

keywords: lakehouse, bucket, catalog, watsonx.data

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

# API change log
{: #api-change-log}

In this change log, you can learn about the latest changes, improvements, and updates for the {{site.data.keyword.lakehouse_full}} APIs. The change log lists the changes in the order of release dates. Changes to existing API versions are compatible with existing client applications.

For instructions on how to update to the latest version of the API, see [Updating to the latest version of the {{site.data.keyword.lakehouse_short}} API](https://cloud.ibm.com/docs/codeengine?topic=codeengine-release-notes).

For information about the latest changes to the {{site.data.keyword.lakehouse_short}} SDKs, see the change logs in the SDK repositories:

* [Java SDK change log](https://github.com/IBM/code-engine-java-sdk/releases)
* [Node SDK change log](https://github.com/IBM/code-engine-node-sdk/releases)
* [Python SDK change log](https://github.com/IBM/code-engine-python-sdk/releases)
* [Go SDK change log](https://github.com/IBM/code-engine-go-sdk/releases)

## API versioning
{: #api-versioning}

API requests require a version parameter that takes the date in the format `version=YYYY-MM-DD`. Send the version parameter with every API request.

When the API is changed in a way that is not compatible with previous versions, a new minor version is released. To take advantage of the changes in a new version, change the value of the version parameter to the new date. If you're not ready to update to that version, don't change your version date.

### Active version dates
{: #active-version-dates}

The following table shows the service behavior changes for each version date. Switching to a later version date activates all changes that are introduced in earlier versions.

| Version date | Summary of changes |
|--------------|--------------------|
| 2024-05-29   | Updated {{site.data.keyword.lakehouse_short}} AMS API. |
| 2023-07-07   | Base version |
{: caption="Table 1. Active version dates" caption-side="bottom"}
