---

copyright:
  years: 2017, 2025
lastupdated: "2025-03-20"

keywords: watsonx.data, spark, emr
subcollection: watsonxdata

---

{{site.data.keyword.attribute-definition-list}}

# Data Access Service (DAS)
{: #cas_ep_ov}

Data Access Service (DAS) proxy in {{site.data.keyword.lakehouse_short}} provides a unified way to access object storage, govern external engines, and audit data access. All of these are accomplished without exposing credentials or requiring complex modifications to engines, which are not controlled by {{site.data.keyword.lakehouse_short}}.
Currently, DAS signature and DAS proxy features are available in {{site.data.keyword.lakehouse_short}}.


The Data Access Service (DAS) proxy feature is completely removed in 2.1.2 and is no longer available in {{site.data.keyword.lakehouse_short}}. You cannot use the Data Access Service (DAS) proxy feature to access object storage (S3, ADLS and ABS).
{: important}


DAS signature is available only internally for Data Stage and IBM Spark. IBM Spark by default connects to the watsonx.data object storage through DAS signature.
{: note}

By using DAS proxy, you can access any S3 or S3 compatible object storage, such as IBM Cloud Object Storage, MinIO, Ceph, and ADLS and ABS compatible storages. If you are using IBM Spark, additional file action capabilities are available.

DAS proxy is a technology preview function, official support will come soon. You can try this preview function and provide feedback.
{: note}

The following topics provide more information about DAS proxy support for different storage types and file action capabilities:
- [Using DAS proxy to access S3 and S3 compatible storages](watsonxdata?topic=watsonxdata-cas_proxy).
- [S3 REST API permissions](watsonxdata?topic=watsonxdata-role_priv#s3restapi).
- [Using DAS to access ADLS and ABS compatible storages](watsonxdata?topic=watsonxdata-cas_proxy_adls).
