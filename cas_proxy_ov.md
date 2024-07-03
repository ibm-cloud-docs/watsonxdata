---

copyright:
  years: 2017, 2024
lastupdated: "2024-07-03"

keywords: watsonx.data, spark, emr
subcollection: watsonxdata

---

{{site.data.keyword.attribute-definition-list}}

# S3 proxy
{: #cas_ep_ov}

S3 proxy in {{site.data.keyword.lakehouse_short}} provides a unified way to access object storage, govern external engines, and audit data access. All of these are accomplished without exposing credentials or requiring complex modifications to engines, which are not controlled by {{site.data.keyword.lakehouse_short}}.
Currently, S3 signature and S3 proxy features are available in {{site.data.keyword.lakehouse_short}}.

S3 signature is available only internally for Data Stage and IBM Spark. IBM Spark by default connects to the watsonx.data object storage through S3 signature.
{: note}

By using S3 proxy, you can access any S3 or S3 compatible object storage, such as IBM Cloud Object Storage, MinIO, and Ceph. If you are using IBM Spark, additional file action capabilities are available.

S3 proxy is a technology preview function, official support will come soon. You can try this technology and provide feedback.
{: note}

- For more information about S3 proxy, see [Using S3 proxy to access S3 and S3 compatible buckets](watsonxdata?topic=watsonxdata-cas_proxy).
- For more information about file actions capabilities, see [S3 REST API permissions](watsonxdata?topic=watsonxdata-role_priv#s3restapi).
