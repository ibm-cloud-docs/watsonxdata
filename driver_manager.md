---

copyright:
  years: 2022, 2025
lastupdated: "2025-06-11"

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

# Driver manager
{: #driver_manager}

The **Driver Manager** within the **Configurations** section of {{site.data.keyword.lakehouse_full}} provides the functionality to add external JDBC drivers (in .jar file format) required for connecting to HANA (using ngdbc 2.17.12) and MySQL (using mysql-connector/j 8.2.0) within {{site.data.keyword.lakehouse_short}}.

The **Driver Manager** now enables both administrator and non-administrator users to view driver details for monitoring purposes, while maintaining appropriate access controls restricted to administrator users only.


## Procedure
{: #driver_manager_prcdr}

To view the details of active drivers, do the following:

1. Log in to the {{site.data.keyword.lakehouse_short}} console.
2. From the navigation menu, select **Configurations** and click **Driver manager**.
3. Click **Add driver** and upload files (.jar file). Then click **Add**.

   This action can only be performed by a admin user. The non-admin users will have only the read-only access.
   {: #note}

4. When the driver validation is completed, click the overflow menu against the driver to assign it to an engine.
