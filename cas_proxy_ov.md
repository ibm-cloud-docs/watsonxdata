---

copyright:
  years: 2017, 2024
lastupdated: "2024-06-12"

keywords: watsonx.data, spark, emr
subcollection: watsonxdata

---

{{site.data.keyword.attribute-definition-list}}

# Content Aware Storage (CAS) overview
{: #cas_ep_ov}

Content Aware Storage (CAS) in {{site.data.keyword.lakehouse_short}} provides a unified way to access object storage, govern external engines, and audit data access. All of these are accomplished without exposing credentials or requiring complex modifications to engines, which are not controlled by {{site.data.keyword.lakehouse_short}}.
Currently, CAS signature and CAS proxy features are available in {{site.data.keyword.lakehouse_short}}.

CAS signature is available only internally for Data Stage and IBM Spark. IBM Spark by default connects to the watsonx.data object storage through CAS signature.
{: note}

By using CAS proxy, you can access any S3 or S3 compatible object storage, such as IBM Cloud Object Storage, MinIO, and Ceph. If you are using IBM Spark, additional file action capabilities are available.

CAS proxy is a technology preview function, official support will come soon. You can try this technology and provide feedback.
{: note}

- For more information about CAS proxy, see [Using CAS proxy to access S3 and S3 compatible buckets](watsonxdata?topic=watsonxdata-cas_proxy).
- For more information about file actions capabilities, see [S3 REST API permissions](watsonxdata?topic=watsonxdata-role_priv#s3restapi).
