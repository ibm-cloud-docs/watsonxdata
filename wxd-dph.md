---

copyright:
  years: 2022, 2025
lastupdated: "2025-04-23"

keywords: watsonx.data, dph, integration
subcollection: watsonxdata

---

{{site.data.keyword.attribute-definition-list}}

# Integrating with DPH
{: #dph_intro}

IBM Data Product Hub as a Service is a self-service solution designed to streamline sharing of data products among data producers and data consumers. This light-weight platform that packages data assets such as SQL queries, and tables into Data products, which servers a specific business use case.
Data consumers can be both technical users and business users.

**Data assets and Data products**

Data assets can be SQL query, SQL table, ML models, or BI dashboards.
Data product is a collection of assets packaged under a platform for a specific business use case.

**Benefits of integration**

   * **Data accessibility** : When watsonx.data integrates with DPH, the metadata information from watsonx.data is packaged as a Data product using presto connector for easy sharing among users. This integration broadens the accessibility of data source in watsonx.data. The data is packaged in a secure manner as it does not involve actual movement of data.
   * **Parameterized querying** : You can package the metadata information of SQL queries in watsonx.data and deliver the results in the formats such as CSV or Parquet.

**Data delivery methods**

   * **Flight service delivery method** : The technical consumers can use Jupyter Notebooks to write a script to access the data sources in watsonx.data.

   * **Data extract delivery method** : The buisness consumers leverage data refinary setvice to extract data from wxd and deliver in the requitred format.
