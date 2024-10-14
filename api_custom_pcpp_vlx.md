---

copyright:
  years: 2017, 2024
lastupdated: "2024-10-10"

keywords: watsonx.data, spark, emr
subcollection: watsonxdata

---

{{site.data.keyword.attribute-definition-list}}

# Velox properties for Presto (C++)
{: #api_custom_pcpp_vlx}

You can customize the Velox properties through an API for Presto (C++).

| Property name | Type | Validation added |
| --- | --- | --- |
| `task_writer_count` | Integer | Limit {1, 1000} |
| `max_split_preload_per_driver` | Integer | Limit {1, 1000} |
{: caption="Velox properties for Presto (C++)" caption-side="bottom"}
