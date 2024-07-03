---

copyright:
  years: 2022, 2024
lastupdated: "2024-07-03"

keywords: architecture, workload isolation

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


# Learning about {{site.data.keyword.lakehouse_short}} architecture and workload isolation
{: #compute_isolation}

## Architecture
{: #compute_arch}

{{site.data.keyword.lakehouse_full}} is a new open architecture that combines the elements of the data warehouse and data lake models. The best-in-class features and optimizations available on the {{site.data.keyword.lakehouse_short}}, make it an optimal choice for next generation data analytics and automation.
{: shortdesc}

It is a multi-tenant system that consists of two major building blocks:
1. Control plane - One control-plane cluster is created per IBM Cloud region that runs multi-tenant components such as service web console UI and API.
2. Data plane - One or more data-plane clusters are connected and managed by a control-plane running single-tenant customer-dedicated components within a customer-isolated instance such as a Presto engine and Hive metastore.

Important components of {{site.data.keyword.lakehouse_short}} are:
1. Web console – Web console is the UI interface for watsonx.data from where customers, can perform various functional tasks. It is a multi-tenant component, which resides in the control plane.
2. Presto - Presto is a distributed SQL query engine, with the capability to query vast data sets located in different data sources.
3. Hive Metastore - Hive metastore (HMS) is a service that stores metadata that is related to presto and other services in a backend relational database. When a new table is created, information that is related to the schema such as column names, data types, are stored in the metastore’s backend database.

## {{site.data.keyword.lakehouse_short}} workload isolation
{: #compute_workload}

As mentioned in the architecture section, some components of IBM® watsonx.data are multi-tenant and shared across customers in a given IBM Cloud region and some are single-tenant where they are explicitly dedicated to customers. To separate the access to infrastructure resources and data, several levels of authentication and authorization checks are in place. IAM authentication and access policies checks are performed on a service level. Role-based access control checks are performed on a resource level to allow only authorized users to perform certain operations and access to data.
