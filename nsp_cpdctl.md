---

copyright:
  years: 2022, 2025
lastupdated: "2025-10-28"

keywords: lakehouse, engine, watsonx.data
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

# Spark table maintenance by using IBM cpdctl
{: #nsp_cpdctl}

**Applies to** : [Spark engine]{: tag-blue}

You can perform Iceberg table maintenance operations by submitting a Spark application with the help of IBM Cloud Pak for Data Command Line Interface (IBM cpdctl). The `tablemaint` utility available in the IBM cpdctl allows you to submit, list, and get the details of a Spark application.
{: shortdesc}

## Before you begin
{: #nsp_cpdctlbyb}

- {{site.data.keyword.lakehouse_short}} instance with Native Spark engine provisioned.
- Download and install IBM cpdctl. For information, see [Installing IBM cpdctl](/docs/watsonxdata?topic=watsonxdata-cpdctl_title).
- Configure the {{site.data.keyword.lakehouse_short}} environment in IBM cpdctl. For information, see [Configure IBM cpdctl](/docs/watsonxdata?topic=watsonxdata-cpdctl_commands_config).

## Table maintenance
{: #nsp_cpdctltm}

You can use the resources available in the tablemaint utility to perform the following table maintenance activities.

- Snapshot management

   * rollback_to_snapshot - Roll back a table to a specific snapshot ID.
   * rollback_to_timestamp - Roll back the table to a snapshot at a specific day and time.
   * set_current_snapshot - Sets the current snapshot ID for a table.
   * cherrypick_snapshot - Cherry-picks changes from a snapshot into the current table state.

- Metadata management

   * expire_snapshots - Remove older snapshots and their files that are no longer needed.
   * remove_orphan_files - Used to remove files that are not referenced in any metadata files of an Iceberg table.
   * rewrite_data_files - Combines small files into larger files to reduce metadata overhead and runtime file open cost.
   * rewrite_manifests - Rewrite manifests for a table to optimize scan planning.

- Table Migration

   * register_table - Creates a catalog entry for a metadata.json file that exists but does not have a corresponding catalog identifier.

For information, see the [How to use wx-data command --help (-h)](/docs/watsonxdata?topic=watsonxdata-cpdctl_commands_wxdata) section.
