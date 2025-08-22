---

copyright:
  years: 2022, 2025
lastupdated: "2025-08-22"

keywords: lakehouse, milvus, watsonx.data

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

# Platform and deployment model comparison
{: #wxd_plfrm_dplmnt_cmpar}

This topic provides the following two tables that outline key features and capabilities of different data deployment models and platforms.

- **[SaaS versus On-Prem deployment comparison](/docs/watsonxdata?topic=watsonxdata-wxd_plfrm_dplmnt_cmpar#wxd_plfrm_dplmnt1)** table focuses on the distinctions between cloud-based (SaaS) and on-premise deployments, covering aspects such as scalability, security, integration, and operational management.
- **[Platform comparison: AstraDB versus IBM® {{site.data.keyword.lakehouse_short}}](/docs/watsonxdata?topic=watsonxdata-wxd_plfrm_dplmnt_cmpar#wxd_plfrm_dplmnt2)** table provides a comparison of selected data platforms, highlighting their architectural approaches, data handling capabilities, query engines, and support for AI and vector-based operations.

## SaaS versus On-Prem deployment comparison
{: #wxd_plfrm_dplmnt1}

| Feature Area | SaaS (Cloud) | On-Prem |
| --- | --- | --- |
| Deployment and Updates | IBM-managed, with automatic updates and scaling. | Self-managed, manual installation, updates, and scaling. |
| Milvus Support | Full Milvus service is available (not just lite Milvus). Lite Milvus is also supported for lightweight vector search needs. | Full Milvus service can be added manually. Lite Milvus is not supported. |
| High Availability and Disaster Recovery (HADR) | Built-in HA and DR features managed by IBM. | Requires manual setup for HA and DR; metadata backup supported. |
| Data Access Service (DAS) | Supported | Supported (in Tech Preview as of version 2.2.x). |
| OpenTelemetry Support | Yes | Yes |
| Governance Integrations (for example, watsonx.governance) | Seamless native integration with IBM governance services. | Possible but requires manual configuration and compatibility setup. |
| Security and IAM | IAM managed through IBM Cloud Identity services with role-based access. | Depends on local authentication (for example, LDAP, AD); custom IAM configuration required. Full control over data, encryption, firewall, and network; aligns with internal security policies. |
| Resource Scaling | Elastic, managed automatically by IBM. | Manual scaling via admin operations and resource management. |
| Service Availability Regions | Restricted to IBM Cloud-supported regions. | Available anywhere customer deploys on-premise. |
| Query Engine - Presto | Available; needs provisioning. IBM manages deployment and scaling. | Available; needs provisioning. Customer manages deployment and scaling. |
| Spark Support (Ingestion) | Available out-of-the-box; used for ingestion and table management. Requires provisioning and setup. | Available out-of-the-box; used for ingestion and table management. Requires provisioning and setup. |
| Storage | Utilizes IBM Cloud Object Storage (COS) – S3-compatible service automatically provisioned by IBM. You pay for storage with flexible scaling. | Uses customer-provided persistent storage via Red Hat OpenShift – typically Ceph, IBM Storage Ceph, or Storage Foundation, set up by the customer. |
| Storage format | Supports both internal COS (automatically provisioned) and a broad range of external object/file stores, including IBM COS, Amazon S3, MinIO, HDFS, Google Cloud Storage, Azure Data Lake, Apache Ozone, NFS, and so forth. | Same wide support as SaaS—built-in and external: IBM COS, S3, Ceph, MinIO, HDFS, Ozone, ADS, Storage Scale, Portworx, NFS, and so forth. |
| Data sources | Supports broad set of connectors—including IBM Cloud services (COS, Db2, Cloud Databases), 3rd-party RDBMS (MySQL, PostgreSQL, SQL Server, Oracle), NoSQL (Cassandra, MongoDB), cloud storage (S3, GCS, Azure), files (FTP, HTTP, Box, Dropbox), Milvus, Elasticsearch, and so forth. | Virtually identical set supported on OpenShift/Pak—covering those same IBM services, relational and NoSQL databases, cloud stores, file connectors, Milvus, and so forth. |
| Custom JDBC connectors | No supported | Supported through Infrastructure Manager |
| Vault and Secret Storage | Not available | Supported |
| Kerberos Auth | Not supported | Supported for connectors |
| Integration |  |  |
| dbt (Data Build Tool) | Supported: dbt‑watsonx‑presto for SQL/Presto, dbt for Spark engine (in‑place transforms). | Supported: dbt‑watsonx‑presto works equally for on‑prem Presto; Spark engine also supports dbt . |
| IBM Knowledge Catalog (IKC) | Native integration for governance on SQL views/tables across Presto/Spark. | Same governance integration applies to on‑prem deployments using IKC . |
| Apache Ranger | Policy support for Presto (C++) and Spark through Ranger plugin. | Also supported on‑prem when Ranger is available in the environment. |
| Databand | Supported for Spark monitoring beyond Spark UI. | Available for on‑prem Spark pipelines too. |
| Birdwatcher | Debugging tool for Milvus service included. | Likely same support for on‑prem since Milvus deployment is similar (documentation not explicit) - Need confirmation. |
| DataStage and Data Virtualization | Integration with IBM DataStage and Data Virtualization on Cloud Pak for Data (CPD). | Fully available in on‑prem installation through Cloud Pak integration. |
| BI Tool Integration | Supports Superset, Tableau, Power BI, Cognos, and so forth through public JDBC/ODBC endpoints. | Same tools supported; depends on local network setup and firewall rules. |
| Manta Lineage Integration | Supported; Built-in integration with visualization in Manta UI. | Supported; Requires manual configuration for Manta integration. |
| Data product hub | Available as a managed service in the cloud. Users can publish, govern, discover, and consume "data products" created within IBM {{site.data.keyword.lakehouse_short}}. Data Product Hub seamlessly integrates with the cloud version for lifecycle management and cataloging. | Also fully supported on-premises as software. Data Product Hub can be deployed within an OpenShift/Cloud Pak for Data environment alongside IBM {{site.data.keyword.lakehouse_short}}. All features such as, data product lifecycle, metadata, governance, search are available natively. |
| Extensibility and BYOL | Limited BYOL (Bring Your Own License) in managed model. | Full BYOL flexibility – integrate any compatible tools or engines. |
| Air-Gap/Offline Usage | Not supported; Requires internet access to use. | Fully supported; Suitable for air-gapped, highly regulated, or disconnected environments. |
| Billing and Licensing | Subscription-based pricing (per usage or per user) | Traditional enterprise license + infrastructure cost |
{: caption="SaaS versus On-Prem deployment comparison" caption-side="bottom"}

## Platform comparison: AstraDB versus {{site.data.keyword.lakehouse_short}}
{: #wxd_plfrm_dplmnt2}

| Category | AstraDB | watsonx.data Enterprise | watsonx.data Enterprise with premium capabilities |
| --- | --- | --- | --- |
| Core architecture | Serverless Cassandra architecture Separated compute and storage Auto-scaling capabilities Multi-cloud deployment | Open data lakehouse architecture Apache Iceberg and Hive metastore Hybrid deployment options Data lake + warehouse benefits | watsonx.data integration watsonx.data intelligence The watsonx.data premium experience is part of the IBM watsonx platform. Multiple integrated experiences on the IBM watsonx platform share services and workspaces. An experience provides focused access to the tools for specific tasks. The IBM watsonx platform includes the following integrated experiences: IBM watsonx.data intelligence IBM watsonx.data integration IBM watsonx.ai IBM watsonx BI |
| Data management | Vector and non-Vector databases Multi-region database deployment Flexible and structured schemas DevOps API to automate operations Bulk loading capabilities Automated backup, restore, and database cloning | Unified control plane Single data access point Support for batch processing, streaming, and data replication Low-cost object storage |  |
| Query engines | APIs, CLI, drivers Data API (Document-based API) clients Cassandra Query Language (CQL) compatibility HTTP access | Presto (Java and C++) Apache Spark Milvus IBM Db2 Warehouse and Netezza integration More than 35 supported database connectors Data virtualization Support for open table formats, including Apache Iceberg |  |
| AI and Vector capabilities | Vector search for AI RAG and ML Embeddings Hybrid search using BM25 and reranking models Natural language search Generative AI optimized Broad ecosystem integration Tight integration with Langflow | Milvus vector database RAG and ML embeddings AI-powered data discovery |  |
| Best use cases | Auto-scaling applications AI and machine learning workloads using vector search Variable usage patterns | Enterprise analytics and AI initiatives | Enterprise analytics and AI initiatives with both structured and unstructured data as well as data governance and data integration requirements. |
{: caption="Platform comparison: AstraDB versus {{site.data.keyword.lakehouse_short}}" caption-side="bottom"}
