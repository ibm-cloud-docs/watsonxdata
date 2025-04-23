---

copyright:
  years: 2022, 2025
lastupdated: "2025-04-23"

keywords: watsonx.data, dph, integration
subcollection: watsonxdata

---

{{site.data.keyword.attribute-definition-list}}

# Integrating with Data Product Hub
{: #dph_intro}

IBM Data Product Hub (DPH) as a Service is a self-service solution designed to streamline sharing of data products between data producers and data consumers. This light-weight platform packages data assets such as SQL queries, and tables into data products, which serves a specific business use case.

Integration of DPH and watsonx.data enables seamless data access between the two services for data engineers.

**Data assets and data products**

Data assets can be SQL queries, SQL tables, ML models or BI dashboards.

Data product is a collection of assets packaged together for a specific business use case.

**Data producers and data consumers**

Data producers are responsible for packaging the data assets into Data products, defining data contract and, making the product accessible to consumers.

Data consumers are the users who subscribe to these Data products. Data consumers can be both technical users and business users.

**Features of integration**

   * **Accessing datasource** : DPH connects with watsonx.data through a Presto connector to create a data asset using the metadata information, which in turn is packaged into a data product. This integration broadens the accessibility of data source in watsonx.data. The data is packaged in a secure manner as it does not involve actual data movement.

      To access data from watsonx.data, do the following:

      1. Create a connection asset to access the data in IBM watsonx.data. To create connection, see [Presto connection](https://dataplatform.cloud.ibm.com/docs/content/wsj/manage-data/conn-watsonxd.html?context=dph&locale=en&audience=wdp).

      1. Create a data product to package the asset. For information, see [Creating a data product directly from a source](https://dataplatform.cloud.ibm.com/docs/content/wsj/data-products/prd_publish_files.html?context=dph&locale=en&audience=wdp).

      1. Publish the data product which will be used by consumers. For more information, see [Publishing your data product](https://dataplatform.cloud.ibm.com/docs/content/wsj/data-products/prd_publish_files.html?context=dph&locale=en&audience=wdp).

   * **Parameterized querying** : You can package the metadata information of SQL queries in watsonx.data and deliver the results in the formats such as CSV or Parquet.

      Data producers can create a data product with customizable query. For information about creating such data products, see [Creating a data product from a customizable query](https://dataplatform.cloud.ibm.com/docs/content/wsj/data-products/prd_publish_customquery.html?context=dph&locale=en&audience=wdp).

**Data delivery methods**

   * **Flight service** : The Flight service provides read access to various data sources in watsonx.data. This delivery method is only used by the technical data consumer. For example, data scientist. Technical consumers can use Jupyter Notebooks to write a script to access the data sources in watsonx.data. For information about Flight services, see [Flight Service](https://dataplatform.cloud.ibm.com/docs/content/wsj/data-products/prd_delivery_methods_overview.html?context=dph&locale=en#flight).

   * **Data extract** : The business consumers use data refinery service to create a CSV data extract file and download it. For information about data extract delivery method, see [Data Extract delivery method](https://dataplatform.cloud.ibm.com/docs/content/wsj/data-products/prd_delivery_methods_overview.html?context=dph&locale=en#extract).
