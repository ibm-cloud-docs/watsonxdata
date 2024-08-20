---

copyright:
  years: 2022, 2024
lastupdated: "2024-08-13"

keywords: watsonxdata, troubleshoot, case sensitivity

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

# Customizing max pool size in Hive Metastore
{: #ts_hive}

You can specify the maximum number of connections in a connection pool that is used by Hive Metastore. Increasing the value of the `max_conn_pool_size` property can increase the maximum number of Spark jobs and clients that can connect to Hive metastore at the same time.

The `max_conn_pool_size` value is set to 10 by default. The configured size is used by two connection pools (`TxnHandler` and `ObjectStore`). When calculating the maximum connection pool size, consider the number of metastore instances and the number of `HiveServer2` instances that are configured with the embedded metastore. For optimal performance, set the configuration to meet the following condition:

```bash
  (2 * pool_size * metastore_instances + 2 * pool_size * HS2_instances_with_embedded_metastore) =
  (2 * physical_core_count + hard_disk_count)
```
{: codeblock}

To increase the value of this property, contact IBM support.
