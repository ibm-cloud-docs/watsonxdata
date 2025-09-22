---

copyright:
  years: 2022, 2025
lastupdated: "2025-09-22"

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

# Amazon S3
{: #amazons_storage}

Amazon Simple Storage Service (Amazon S3) is an object storage service that offers industry-leading scalability, data availability, security, and performance.
{: shortdesc}

If you select **Amazon S3** from the **Storage** section, configure the following details:

 | Field | Description |
 |--------------------------|----------------|
 | Display name | Enter the name to be displayed.|
 | Bucket name | Enter your existing object storage bucket name.|
 | Region | Select the region where the storage is available.|
 | Endpoint | Enter the endpoint URL.|
 | Access key | Enter your access key. |
 | Secret key | Enter your secret key. |
 | Role ARN (Amazon Resource Name)  | Identifies an IAM (Identity and Access Management) role that a service or user can assume to gain temporary access to AWS (Amazon Web Services) resources. This field is optional. Specify the Role ARN in the format: `arn:aws:iam::<AWS_ACCOUNT_ID>:role/<ROLE_NAME>`. For example, `arn:aws:iam::123456789012:role/MyExampleRole`. |
 | Connection Status | Click the Test connection link to test the storage connection. If the connection is successful, a success message appears.|
 | Designate this bucket as the ACL store | Select the checkbox to designate this bucket as the ACL store. \n This feature applies to {{site.data.keyword.lakehouse_short}} Premium, for more information see [Governance through Access Controlled Lists (AC)](https://dataplatform.cloud.ibm.com/docs/content/wsj/wx-data/gov_acl.html?context=wxd&audience=wdp). If you select the checkbox, the Associate catalog option is automatically selected, and you must specify a catalog to be used for ACLs.|
 | Associate Catalog | Select the checkbox to add a catalog for your storage. This catalog is associated with your storage and serves as your query interface with the data stored within. |
 | Catalog type | Select the catalog type from the list. The recommended catalog is Apache Iceberg. The other options for catalog are Apache Hive, Apache Hudi, and Delta Lake.|
 | Catalog name | Enter the name of your catalog.|
 | Associate | Click Associate to create the storage. |
 {: caption="Register bucket" caption-side="bottom"}

If Amazon S3 is already inactive in old instances, the system will display the `Activate` button. Once you activate Amazon S3, the system will automatically remove the `Activate` button.
{: note}
