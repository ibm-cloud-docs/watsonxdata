---

copyright:
  years: 2017, 2024
lastupdated: "2024-08-02"

keywords: watsonx.data, spark, analytics, provisioning
subcollection: watsonxdata

---

{{site.data.keyword.attribute-definition-list}}

# Provisioning Native Spark engine
{: #prov_nspark}

{{site.data.keyword.lakehouse_full}} allows you to provision Native Spark engine to run complex analytical workloads.

## Before you begin
{: #prereq_nspark_prov}


1. Create a new Cloud Object Storage and a bucket (you can also use an existing COS bucket if you have one). For more information, see [Creating a storage bucket][def]. This storage is considered as Engine home, which stores the Spark events and logs that are generated while running spark applications.
1. Register the Cloud Object Storage bucket. For more information, see [Adding a storage-catalog pair](watsonxdata?topic=watsonxdata-reg_bucket).

## Procedure
{: #pros_nspark_prov}



To provision a natice Spark engine, see [Provisioning a Spark engine](watsonxdata?topic=watsonxdata-spl_engine).



[def]: https://cloud.ibm.com/docs/cloud-object-storage?topic=cloud-object-storage-secure-content-store#create-cos-bucket
