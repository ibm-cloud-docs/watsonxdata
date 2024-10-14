---

copyright:
  years: 2022, 2024
lastupdated: "2024-09-30"

keywords: watsonx.data, ikc, configuring, knowledgecatalog
subcollection: watsonxdata

---

{{site.data.keyword.attribute-definition-list}}

# Integrating with DataStage
{: #dc_integration}

You can integrate {{site.data.keyword.lakehouse_full}} with IBM DataStage on Cloud Pak for Data to ingest and to read data from {{site.data.keyword.lakehouse_short}}.

## Requirements
{: #prereq_ds}

Following are the requirements to integrate {{site.data.keyword.lakehouse_short}} with DataStage:

- Cloud Pak for Data with DataStage (version 5.0.1 or later)
- {{site.data.keyword.lakehouse_full}} (version 2.0.0 or later)
- Use {{site.data.keyword.lakehouse_short}} connector in DataStage to read or ingest data into {{site.data.keyword.lakehouse_short}}.
- Make sure that Data Access Service (DAS) is enabled in {{site.data.keyword.lakehouse_short}} to enable data ingestion in DataStage.
- Presto engine must be provisioned in {{site.data.keyword.lakehouse_short}} to read and ingest data in DataStage.
- Amazon S3 or IBM Cloud Object storage must be connected to {{site.data.keyword.lakehouse_short}} to enable data ingestion in DataStage.
- The Amazon S3 or IBM Cloud Object storage must be connected to the Iceberg catalog, which must be associated to the Presto engine to enable data ingestion in DataStage.

For more information about connecting to a data source in DataStage, see [Connecting to a data source in DataStage](https://www.ibm.com/docs/en/cloud-paks/cp-data/5.0.x?topic=connectors-connecting-data-source-in-datastage).

For more information about creating a connection asset in watsonx.data, see [IBM watsonx.data connection](https://www.ibm.com/docs/en/cloud-paks/cp-data/5.0.x?topic=connectors-watsonxdata-connection).
