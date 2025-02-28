---

copyright:
  years: 2017, 2024
lastupdated: "2025-02-19"

keywords: watsonx.data, spark, analytics, provisioning
subcollection: watsonxdata

---

{{site.data.keyword.attribute-definition-list}}

# Why is Milvus data missing or corrupted?
{: #milvus_data_miss_ts}
{: troubleshoot}

The data present in the customer's Milvus bucket is either missing or corrupted.
{: tsSymptoms}


There can be several reasons of missing or corrupted data in Milvus. The data may be deleted or the association of the created bucket policy has expired.
{: tsCauses}

Make sure that you have already enabled replication for the primary Milvus bucket to ensure that the backup bucket contains the same data as the primary bucket.
{: tsResolve}

In the case of data corruption or missing in Milvus, contact IBM support to recover the data.
