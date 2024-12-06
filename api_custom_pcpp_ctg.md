---

copyright:
  years: 2017, 2024
lastupdated: "2024-12-06"

keywords: watsonx.data, spark, emr
subcollection: watsonxdata

---

{{site.data.keyword.attribute-definition-list}}

# Catalog properties for Presto (C++)
{: #api_custom_pcpp_ctg}

You can customize the catalog properties through an API for Presto (C++).

| Property name | Type | Validation added |
| --- | --- | --- |
| `hive.orc.use-column-names` | Boolean | True or False |
| `hive.parquet.use-column-names` | String | Any string |
| `max-partitions-per-writers` | Integer | Limit{1, 100000} |
| `file-column-names-read-as-lower-case` | Boolean | True or False |
{: caption="Catalog properties for Presto (C++)" caption-side="bottom"}

The `file-column-names-read-as-lower-case` property is set to `False` by default on Presto (C++) worker and must not be set to `True`. This property must not be set anywhere else because it might cause the engine to crash.
{: note}
