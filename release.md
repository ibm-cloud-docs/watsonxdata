---

copyright:
  years: 2023, 2024
lastupdated: "2025-07-07"

keywords: watsonxdata, release notes

subcollection: watsonxdata

content-type: release-note

---


{{site.data.keyword.attribute-definition-list}}

# Release notes for {{site.data.keyword.lakehouse_short}}
{: #release}

Use these release notes to learn about the latest updates to {{site.data.keyword.lakehouse_full}} that are grouped by date.
{: shortdesc}


For watsonx.data as a Service on IBM Cloud with gen AI experience what's new, see [Release notes for watsonx.data as a Service on IBM Cloud with gen AI experience](https://dataplatform.cloud.ibm.com/docs/content/wsj/wx-data/whats_new-wdp.html?context=wxd&audience=wdp).

For watsonx.data on-prem what's new, see [Release notes for watsonx.data](https://www.ibm.com/docs/en/watsonx/watsonxdata/2.2.x?topic=overview-whats-new-in-watsonxdata).

For watsonx.data on-prem Premium what's new, see [Release notes for on-prem Premium](https://www.ibm.com/docs/en/watsonx/watsonxdata-premium/2.2.x?topic=overview-whats-new-in-watsonxdata).


## 07 July 2025 - Version 2.2 Hotfix 1
{: #lakehouse_07july2025}
{: release-note}

Version 2.2 hotfix of watsonx.data was released on 07 July, 2025. This release includes security updates and fixes.

## 11 June 2025 - Version 2.2
{: #lakehouse_11june212}
{: release-note}



Engine and service enhancements

: This release of {{site.data.keyword.lakehouse_short}} introduces the following engine and service enhancement:

   * Introduced new API versions for connecting to a Milvus service by using a proxy host route. For more information, see [Connecting to Milvus service](/docs/watsonxdata?topic=watsonxdata-conn-to-milvus).
   * For the Presto (C++) engines, the Hive and Iceberg catalogs are now enabled with region configuration. For more information, see [Provisioning a Presto (C++) engine](/docs/watsonxdata?topic=watsonxdata-pcpp_prov).
   * New Gluten accelerated Spark engine: You can now provision Gluten accelerated Spark engine and use it to run complex analytical workloads by leveraging high scalability of Spark SQL framework and high performance of native libraries. For information about working with the new Gluten accelerated Spark engine, see [Working with Gluten accelerated Spark engine](/docs/watsonxdata?topic=watsonxdata-prov_cpp).
   * Run faster workspace queries by using a Spark job to transform Iceberg table data : To speed up the reading of Iceberg tables, you can now use a Spark job to transform Iceberg table data from Merge-on-Read (MOR) format to Copy-on-Write (COW) format. For more information, see [Submitting Spark jobs for MoR to CoW conversion](/docs/watsonxdata?topic=watsonxdata-sbmt_spk_mor_cow).
   * You can use the Spark API functionality to configure the limit of applications that can be listed and the filter criteria that you can use to filter the Spark applications.

CPDCTL CLI enhancements
: This release of watsonx.data introduces the following enhancements to IBM Cloud Pak for Data Command Line Interface (IBM cpdctl):

   * You can use the tablemaint command to execute different Iceberg table maintenance operations in watsonx.data.

   * You can use the wx-data service command to perform various serviceability related operations, such as listing tables, retrieving the list of QHMM enabled buckets, and monitoring QHMM related statistics and queries.

   For more information, see [IBM cpdctl](/docs/watsonxdata?topic=watsonxdata-cpdctl_title).


Integration enhancements
: This release of watsonx.data introduces the following enhanced integration with other services:
   * New delivery method: Deliver as a table in watsonx.data

   Data products using supported data sources can now be delivered to your instance of watsonx.data tables by using the deliver as a table in watsonx.data method. This method allows users with the appropriate permissions to create new tables or append to existing ones. For more information, see [Integrating with Data Product Hub](/docs/watsonxdata?topic=watsonxdata-dph_intro).

   * New delivery method: Access in watsonx.data

   You can now subscribe to a data product created from the watsonx.data instance by using the access in watsonx.data delivery method. This method lets consumers directly access watsonx.data resources through Data Product Hub. After delivery, consumers will see details on how to access the watsonx.data instance and the specific resources they have access to. For more information, see [Integrating with Data Product Hub](/docs/watsonxdata?topic=watsonxdata-dph_intro).

   * You can now connect to the Spark query server in the following ways and execute queries to analyze your data.

      * Using DBeaver (JDBC clients)
      * Using Java (JDBC Client) code
      * Using Python (PyHive JDBC Client)

      For more information, see [Connecting to Spark query server by using Spark JDBC Driver](/docs/watsonxdata?topic=watsonxdata-dbt_watsonx_connt).

Billing enhancements
: This release of watsonx.data introduces the following enhancements to the billing feature:

   * Billing granularity: Users will now be able to view their billing statements in an itemized format, offering greater granularity and transparency
   * Billing accuracy: User billing usage will now be tracked at a per-minute level, replacing the previous high-watermark method

Query History Monitoring and Management (QHMM) enhancement

: This release of {{site.data.keyword.lakehouse_short}} introduces the following QHMM enhancement:

   The Query monitoring page is removed from the Quick start wizard setup and is consolidated with the Configure a bucket page. You can now enable, disable, configure the QHMM storage details directly from the updated Configure a bucket page available in the Quick start wizard. For information about the updated Quick start wizard setup, see [Quick start](/docs/watsonxdata?topic=watsonxdata-quick_start_213).

Data sources and storage enhancements

: This release of {{site.data.keyword.lakehouse_short}} includes the following storage enhancement:

   You can now use the SQL Server with New Technology LAN Manager (NTLM) authentication and Microsoft Entra authentication. NTLM is a windows based challenge - response authentication method. For more information, see [SQL Server](/docs/watsonxdata?topic=watsonxdata-sqlserver_database).


Access management enhancements

: This release of {{site.data.keyword.lakehouse_short}} introduces the following access management enhancements:

   * You can use the export functionality to download the existing resource policies and import them into another required environment. This ensures consistency and helps smooth migration. For information about how to use the import export functionality, see [Managing user access](/docs/watsonxdata?topic=watsonxdata-manage_access).
   * A catalog administrator or a user who belongs to a group with an admin role can now remove their access to the catalog. For more infromation about how to remove a user for a component, see [Managing user access](/docs/watsonxdata?topic=watsonxdata-manage_access).
   * Non-admin users has read-only access and can now view the Driver Manager page within the Configurations section. This allows them to see the list of active drivers and their details without needing to consult an administrator. For more information, see [Driver manager](/docs/watsonxdata?topic=watsonxdata-driver_manager).

Auditing and tracking enhancements

: This release of {{site.data.keyword.lakehouse_short}} introduces the following auditing and tracking enhancement:

   The list of trackable events now includes detailed activities related to the MDS Thrift server and the MDS Rest server providing insights into how applications and users are interacting with these critical components. For information, see [MDS Thrift server events](/docs/watsonxdata?topic=watsonxdata-at_events#at_actions_mdsthrift) and [MDS Rest server events](/docs/watsonxdata?topic=watsonxdata-at_events#at_actions_mdsrest).


Deprecated features

: The following features are deprecated in this release:

   * The Milvus APIs that use the REST host (APIs with the /api/v1 prefix) are deprecated as of {{site.data.keyword.lakehouse_short}} v2.2.

   * Azure Data Lake Storage (ADLS) Gen1 is now deprecated and will be removed in an upcoming release. You must transition to ADLS Gen2 because ADLS Gen1 is not available.

   * The user authentication method of using ibmlhapikey and ibmlhtoken as the username is now deprecated and shall be removed in a future   release. You can use ibmlhapikey_username and ibmlhtoken_username instead. For more infromation, see [Access management and governance in watsonx.data](/docs/watsonxdata?topic=watsonxdata-access_mgt).



## 10 April 2025 - Version 2.1.2 Hotfix 1
{: #lakehouse_9apr2121}
{: release-note}

Engine and service enhancements

: This release of {{site.data.keyword.lakehouse_short}} introduces the following service enhancement:

   Introduced Tiny Milvus, a lightweight, single-node deployment of the Milvus vector database, which is tailored for experimentation and early-stage development.

   Tiny Milvus provides the core Milvus experience and is designed specifically for use within the watsonx.ai platform. It serves as an entry point for vector-based AI exploration with minimal resource requirements to help ensure effective data management and analysis. It is distinct from other Milvus configurations available within {{site.data.keyword.lakehouse_short}}, which support broader scalability and enterprise-grade features.

   Tiny Milvus supports up to 10K vectors, making it suitable for quick trials and early experimentation without heavy infrastructure. It is not intended for production workloads.

   For more information about using Tiny Milvus, see [Setting up a watsonx.data Milvus vector store](https://dataplatform.cloud.ibm.com/docs/content/wsj/analyze-data/fm-prompt-data-index-milvus.html?context=wx){: external}.



## 04 April 2025 - Version 2.1.2
{: #lakehouse_2apr212}
{: release-note}

{{site.data.keyword.lakehouse_short}} 2.1.2 version is releasing to different geographic regions in stages and is not available in all regions. To know if the 2.1.2 release is available in your region, contact IBM Support.
If you are currently using {{site.data.keyword.lakehouse_short}} 2.1.1 version, you can refer to the documentation, [watsonx.data 2.1.1](https://ibm.ent.box.com/s/zgw7umzibl9akxgi7vm4yxs4vyp8io6g).
{: important}

Data sources and storage enhancements

: This release of {{site.data.keyword.lakehouse_short}} includes the following storage enhancement:

   Now you can connect to **IBM Db2 for i** data source. For information about **IBM Db2 for i**, see [IBM Db2 for i](/docs/watsonxdata?topic=watsonxdata-bd2fori_database).

Connectivity enhancements

: This release of {{site.data.keyword.lakehouse_short}} includes the following Connectivity enhancement:

   You can now securely and privately connect to a {{site.data.keyword.lakehouse_short}} instance by using virtual private endpoints. For information about configuring network endpoints in {{site.data.keyword.lakehouse_short}}, see [Setting up virtual private endpoints](/docs/watsonxdata?topic=watsonxdata-setup_vpe).

Integration enhancements

: This release of {{site.data.keyword.lakehouse_short}} introduces the following enhanced integrations with other services:

   * Now, you can define IBM Knowledge Catalog governance policies for Presto (C++) engine when you integrate with {{site.data.keyword.lakehouse_short}}. For information about connecting to IBM Knowledge Catalog (IKC), see [Connecting to IBM Knowledge Catalog (IKC)](/docs/watsonxdata?topic=watsonxdata-ikc_integration).
   * You can now export configuration files for target Presto engine, based on their ODBC driver selection (Simba or CData), to more easily establish connections with {{site.data.keyword.lakehouse_short}}. This enhancement saves you from manually configuring Presto engine details by using PowerBI. For more information about connecting to Presto by using the Config files, see [Connecting to Presto by using the Config files](/docs/watsonxdata?topic=watsonxdata-bi_intro#confug_file).
   * Integrating with Data Product Hub: You can integrate {{site.data.keyword.lakehouse_short}} with DPH to package SQL tables and queries into data products tailored for specific use cases. For details, see [Integrating with Data Product Hub](/docs/watsonxdata?topic=watsonxdata-dph_intro).

Ingestion enhancement

: This release of {{site.data.keyword.lakehouse_short}} includes the following Ingestion enhancement:

Ingestion jobs using an external Spark engine now provide logs within {{site.data.keyword.lakehouse_short}}. This enhancement allows users to effectively identify and troubleshoot job execution directly within the {{site.data.keyword.lakehouse_short}} on cloud platform (SaaS instance). The details of the ingestion procedure is available in [Ingesting data by using Spark through the web console](/docs/watsonxdata?topic=watsonxdata-ingest_spark_ui).

Engine and service enhancements

: This release of {{site.data.keyword.lakehouse_short}} introduces the following engine and service enhancement:

   You can now use the Azure Data Lake Storage Gen2 with AccessKey Authmode with Spark engine to store your data while submitting Spark applications. For information about Azure Data Lake Storage Gen2, see [Azure Data Lake Storage](/docs/watsonxdata?topic=watsonxdata-adls_genblob_storage).

Query workspace enhancements

: This release of {{site.data.keyword.lakehouse_short}} introduces the following query workspace enhancement:

   You now have the option to cancel one or multiple running queries. Additionally, you can remove queries from the worksheet after they are canceled or successfully completed, making it easier to keep your workspace organized. For more information, see [Running SQL queries](watsonxdata?topic=watsonxdata-run_sql).


Access management enhancements

: This release of {{site.data.keyword.lakehouse_short}} introduces the following access management enhancements:

   * Administrators can now configure access for IBM Db2 and IBM Netezza. They can assign roles for {{site.data.keyword.lakehouse_short}} users to view, edit, and administer the IBM Netezza and IBM Db2 engines. For information about the resource-level permissions, see [(Db2 and Netezza)](/docs/watsonxdata?topic=watsonxdata-role_priv#db2_net).
   * Administrators can now grant or revoke specific permissions to users or roles when creating and viewing their own schemas. For information about data policy rules, see [Managing data policy rules](/docs/watsonxdata?topic=watsonxdata-data_policy).
   * DAS proxy flow, which was previously deprecated, is now removed and is no longer available in {{site.data.keyword.lakehouse_short}}.

Query History Monitoring and Management (QHMM) enhancement

: This release of {{site.data.keyword.lakehouse_short}} introduces the following QHMM enhancements:

   * You can now select the Presto engine that is associated to a QHMM catalog when you configure query monitoring in {{site.data.keyword.lakehouse_short}}. For information about configuring QHMM, see [Configuring query monitoring](/docs/watsonxdata?topic=watsonxdata-qhmm).
   * You can now use the migration script to transfer QHMM data from the source bucket to the destination bucket in {{site.data.keyword.lakehouse_short}}. For more information about using the migration script, see [QHMM Shell Script usage](/docs/watsonxdata?topic=watsonxdata-qhmm_shell).

CPDCTL CLI enhancements

: This release of {{site.data.keyword.lakehouse_short}} introduces the following enhancements to IBM Cloud Pak for Data Command Line Interface (IBM cpdctl):

   * Starting in version 2.1.2, the `wx-data` command is available by default, which enables you to do operations such as, ingesting, managing engines, and so on, in {{site.data.keyword.lakehouse_short}}.
   * You can use the `wx-data engine create` and `wx-data engine delete` commands to provision and delete all available engines in {{site.data.keyword.lakehouse_short}}.
   * You can use the `sparkjob` command to submit, list, and get the details of a Spark application.
   * `INSTANCE_ID` used in setting the instance environment is replaced with `WX_DATA_INSTANCE_ID`.

   For more information, see [IBM cpdctl](https://www.ibm.com/docs/SSDZ38_2.1.x/wxd-client/topics/cpdctl-title.html).

## 28 February 2025 - Version 2.1.1
{: #lakehouse_28feb211}
{: release-note}

New region availability

: {{site.data.keyword.lakehouse_short}} is now available in Toronto region for Lite and Enterprise plans. To provision, see [Provisioning watsonx.data Lite plan](/docs/watsonxdata?topic=watsonxdata-tutorial_prov_lite_1) and [Provisioning watsonx.data Enterprise plan](/docs/watsonxdata?topic=watsonxdata-getting-started_1).


Data sources and storage enhancements

: This release of {{site.data.keyword.lakehouse_short}} includes the following storage enhancements:

   * Now, you can test connections for the following data sources and storage:

      * Apache Phoenix
      * IBM Data Virtualization Manager
      * BigQuery
      * Google Cloud Storage
   * You can now register and load external pre-existing Hudi and Delta tables on an object storage by using [Register table](https://cloud.ibm.com/apidocs/watsonxdata-software#register-table) and [load table metadata](https://cloud.ibm.com/apidocs/watsonxdata-software#load-table) APIs.

Ingestion enhancement

: After an ingestion job is completed, you can now access the ingested data directly from the **Ingestion History** page, which streamlines your workflow and saves time.

Integration enhancements

: This release of {{site.data.keyword.lakehouse_short}} introduces the following enhanced integrations with other services:


   - The **Connection Information** page now includes:
      * Presto configuration details for DBT integration. You can copy the Presto configuration details that are required for DBT integration from this page.
      * Option to export the TDS file, which includes the Presto engine configuration details that are required for Tableau integration.

   For more information, see [Getting connection information](/docs/watsonxdata?topic=watsonxdata-get_connection).

Engine and service enhancements

: This release of {{site.data.keyword.lakehouse_short}} introduces the following engine and service enhancements:

   - You can now create a Spark application from the **Applications** tab of the Spark engine details page. For more information, see [Submitting Spark application from Console](/docs/watsonxdata?topic=watsonxdata-smbit_cnsl_1).
   - You can now use Spark version, 3.5.4 to run the applications in {{site.data.keyword.lakehouse_short}}. In {{site.data.keyword.lakehouse_short}}, Apache Spark 3.4.4 and Apache Spark 3.5.4 are the supported versions.
   - Milvus allows the following:
      - In Milvus you can now do a hybrid GroupBy search based on multiple vector columns and also customize the group size when you run search queries. For more information, see [Connecting watsonx Assistant to watsonx.data Milvus for custom search](/docs/watsonxdata?topic=watsonxdata-wxd_wxa_connection).
      - Milvus now supports custom size with a capacity of 3 billion vectors with a maximum of 1,024 dimensions.
      - Milvus now allows scaling up or down between predefined T-shirt sizes (small, medium, and large) or custom sizes. For more information, see [Adding Milvus service](/docs/watsonxdata?topic=watsonxdata-adding-milvus-service).
   - Starting from {{site.data.keyword.lakehouse_short}} 2.1.1 version, Milvus 2.5.0 is supported. For more information, see [Milvus](/docs/watsonxdata?topic=watsonxdata-whatismilvus).

Access management enhancements

: This release of {{site.data.keyword.lakehouse_short}} introduces the following access management enhancements:

   - The Access Management Service (AMS) in {{site.data.keyword.lakehouse_short}} can now use JSON Web Token (JWT) authentication for incoming requests from Presto, ensuring secure and efficient access control. For more information, see [Connecting to Presto engine through Presto CLI (Remote)](/docs/watsonxdata?topic=watsonxdata-con-presto-serv#conn-to-prestoeng).
   - You can now assign users and roles to infrastructure components in batches of Twenty. For more information, see [Managing user access](/docs/watsonxdata?topic=watsonxdata-manage_access).
   - You can now use Apache Ranger Hadoop SQL policies to govern data with Spark engines. You can define Ranger policies when the Spark engine accesses data from Hadoop clusters. Enabling Ranger policy ensures robust data security and governance. With the Ranger policy, you can configure table authorization (L3), row-level filtering, and column masking for data. For more information, see [Enabling Apache Ranger policy for resources](/docs/watsonxdata?topic=watsonxdata-ranger_1).

CPDCTL CLI enhancements

: IBM `CPDCTL` CLI is now used to configure and manage different operations in {{site.data.keyword.lakehouse_short}}. Using the `CPDCTL` CLI, you can manage configuration settings, run ingestion jobs, manage engines, data sources, and storages. The following two plugins are currently used to execute these operations:

   * `config` - To configure {{site.data.keyword.lakehouse_short}} service environment and users.
   * `wx-data` - To perform other operations such as, ingesting, managing engines, etc in {{site.data.keyword.lakehouse_short}}. For more information, see [IBM cpdctl](https://www.ibm.com/docs/en/watsonx/watsonxdata/2.1.x?topic=cloud-pak-data-command-line-interface-cpdctl).

      {{site.data.keyword.lakehouse_short}} developer edition is now enabled in IBM CPDCTL version v1.6.104 and later.
      {: note}

Deprecated features

: The following features are deprecated in this release:

   * The Data Access Service (DAS) proxy feature is now deprecated and will be removed in a future release. You cannot use the Data Access Service (DAS) proxy feature to access object storage (S3, ADLS and ABS). If you use DAS proxy flow and face any issues, contact IBM support. For an overview of the DAS feature, see [Data Access Service (DAS)](/docs/watsonxdata?topic=watsonxdata-cas_ep_ov).

   * IBM Client package is now deprecated and shall be removed in a future release. The utilities and commands in Client package is replaced with IBM CPDCTL CLI. For more information about how to use IBM CPDCTL CLI, see [IBM cpdctl](https://www.ibm.com/docs/en/watsonx/watsonxdata/2.1.x?topic=cloud-pak-data-command-line-interface-cpdctl).

## 04 February 2025 - Version 2.1.0 Hotfix 2
{: #lakehouse_04febhf}
{: release-note}

Lite plan enhancement

: {{site.data.keyword.lakehouse_full}} Lite plan is now available in the Sydney region. For more information to provision a Lite plan instance in Sydney region, see [Provisioning Lite plan](https://cloud.ibm.com/docs/watsonxdata?topic=watsonxdata-tutorial_prov_lite_1#create-lite-cli).

## 10 January 2025 - Version 2.1.0 Hotfix 1
{: #lakehouse_09janhf}
{: release-note}

Enterprise plan enhancement

: If you use IBM Cloud CLI to provision an Enterprise plan instance in the Sydney region, you must use the plan name `lakehouse-enterprise-mcsp`. For more information, see [Provision an instance through CLI](/docs/watsonxdata?topic=watsonxdata-getting-started_1#create-by-cli).

## 13 December 2024 - Version 2.1.0
{: #lakehouse_12Dec21}
{: release-note}

Data sources and storage enhancements

: This release includes the following new data sources and storage enhancements:

   * Now you can connect to Apache Phoenix data sources. For more information, see [Apache Phoenix](/docs/watsonxdata?topic=watsonxdata-phoenix_database)

   * If you work with MySQL data sources, now you can manage drivers in the **Driver manager** section of the Configurations page. Each of these drivers goes through a series of validation steps. You can no longer test MySQL connections. For more information, see [MySQL](/docs/watsonxdata?topic=watsonxdata-mysql_database).

   When you upgrade to version 2.1.0, any existing MySQL catalog is no longer linked to the engine. This means that you need to reestablish the connection between the MySQL catalog and the engine.
   {: note}

   * Test connection feature is now available for the following data sources supported by Arrow Flight service:

      * Apache Derby
      * Salesforce
      * Greenplum
      * MariaDB

   * Now you can test connection for Azure Data Lake Storage (ADLS) and IBM Data Virtualization Manager for z/OS data source.

Integration enhancements

: This release of {{site.data.keyword.lakehouse_short}} introduces the following new or enhanced integrations with other services:

   * You can now enable Databand connection from the **Configurations** page. For more information, see [Monitoring Spark application runs by using Databand](/docs/watsonxdata?topic=watsonxdata-mntr_dband).

   * You can now retrieve the Presto connection information from the {{site.data.keyword.lakehouse_short}} instance > **Configurations** > **Connection information** page for the following integration:

      * BI tools
      * DataBuildTool (dbt)

   * Starting with {{site.data.keyword.lakehouse_short}} version 2.1, you can only integrate with one of the following policy engines:

      * Apache Ranger
      * IBM Knowledge Catalog (IKC)

   For more information, see [Connection information](/docs/watsonxdata?topic=watsonxdata-get_connection).

   * You can now integrate IBM Manta Data Lineage with {{site.data.keyword.lakehouse_short}} to capture and publish jobs, runs, and dataset events from Spark through the Manta UI. For more information, see [IBM Manta Data Lineage](/docs/watsonxdata?topic=watsonxdata-manta_overview).

   * You can now use all of the Presto data types with the dbt adapter for Presto. Specify the data type as column_types in the dbt_project.yml. For more information, see [Installing and using dbt-watsonx-presto](/docs/watsonxdata?topic=watsonxdata-dbt_watsonx_presto_inst).

Engine and service enhancements

: This release of {{site.data.keyword.lakehouse_short}} introduces the following engine and service enhancements:

   * You can now use the Azure Data Lake Storage Gen2 with AccessKey Authmode and Google Cloud Storage with Presto (C++) engine. You can now use Azure Data Lake Storage (ADLS) and Google Cloud Storage to store your data while submitting Spark applications. For more information, see [Azure Data Lake Storage](/docs/watsonxdata?topic=watsonxdata-adls_genblob_storage) and [Google Cloud Storage](/docs/watsonxdata?topic=watsonxdata-gcs_storage).

   * You can now use Google Cloud Storage (GCS) with Data Access Service (DAS) to store your data while submitting Spark applications. For more information, see [Submitting Spark application by using native Spark engine](/docs/watsonxdata?topic=watsonxdata-smbit_nsp_1).

   * You can now enable the Spark Access Control extension to access and operate on the Hive and Hudi catalogs. For more information, see [Enhancing Spark application submission using Spark access control extension for external Spark](/docs/watsonxdata?topic=watsonxdata-spark-extnsn_ext) and [Enhancing Spark application submission using Spark access control extension for native Spark](/docs/watsonxdata?topic=watsonxdata-spark-extnsn).

   * You can now select a {{site.data.keyword.lakehouse_short}} Spark engine as a runtime environment in watsonx.ai notebooks. This allows you to run Jupyter notebooks on your {{site.data.keyword.lakehouse_short}} native Spark engine. For more information, see [Working with watsonx.ai Notebooks](/docs/watsonxdata?topic=watsonxdata-run_nbwxai).


   * Presto administrators can now configure JMX metrics through API. Currently, Only alphanumeric characters are allowed for the key in JMX property names. For more information, see [Update presto engine](https://cloud.ibm.com/apidocs/watsonxdata#update-presto-engine){: external}.

Query history information by using ibm-lh utility

: You can get the following Query history information by using ibm-lh utility:


   * Basic query information.
   * Basic error information of failed queries.
   * Query stats information.
   * Query memory information.
   * Query garbage collection information.
   * Top time taken query.
   * Memory usage details of queries.
   * Information after joining the two tables.
   * Information containing all the columns of a table.
   * Information about the errors in the query.
   * Count of all error codes.
   * Count of all failure messages.
   * Count of all failure types.

For more information, see [Retrieving QHMM logs by using ibm-lh utility](/docs/watsonxdata?topic=watsonxdata-qhmm_ret).

Ingestion enhancements

: This release of {{site.data.keyword.lakehouse_short}} introduces the following ingestion enhancements:

   * **Target table preview**: Before submitting an ingestion job, users can now preview the target table schema and edit the column headers and data types. This allows for validation and ensures data is ingested into the correct table structure. For more information, see [Ingesting data by using Spark through the web console](/docs/watsonxdata?topic=watsonxdata-ingest_spark_ui).

   * **Java/Spark-based ingestion for table creation**: The Data Manager now includes an option to create tables using the Java/Spark-based ingestion flow navigating to Local ingestion, providing flexibility and control based on file size and other factors. For more information, see [Creating table](/docs/watsonxdata?topic=watsonxdata-create_table) and [Ingesting data by using Spark through the web console](/docs/watsonxdata?topic=watsonxdata-ingest_spark_ui).

   * **Enhanced source storage support**:
       * Azure Data Lake Storage (ADLS): Support for ingesting data directly from ADLS is now available.
       * Google Cloud Storage (GCS): Support for ingesting data directly from GCS is now available.

   * **Transient storage**: Users can now select the external bucket to use as a staging area for local ingestions. If no storage is specified, {{site.data.keyword.lakehouse_short}} can infer and select an appropriate bucket. For more information, see [Ingesting data by using Spark through the web console](/docs/watsonxdata?topic=watsonxdata-ingest_spark_ui).

Introduction to Metadata Service (MDS)

: Starting from the 2.1 release, {{site.data.keyword.lakehouse_short}} uses Metadata Service (MDS) instead of Hive Metastore (HMS). MDS is compatible with modern, open catalog APIs, Unity Catalog API, and Apache Iceberg REST Catalog API, enabling wider tool integration and increased flexibility. This new architecture delivers comparable performance while it continues to support Spark and Presto clients through the existing Thrift or HMS interface. For more information, see [Metadata Service (MDS) overview](/docs/watsonxdata?topic=watsonxdata-mdsov).

It is recommended to use MDS in your test environments and then move to using it in production.
{: note}

Deprecated features

: The following feature is deprecated in this release:

   * The REST API feature to capture DDL changes in {{site.data.keyword.lakehouse_short}} through the event listener will be deprecated from {{site.data.keyword.lakehouse_short}} release version 2.1.

## 13 November 2024 - Version 2.0.4 Hotfix
{: #lakehouse_13Novhf}
{: release-note}

Lite plan enhancements

: This hotfix release includes the following Lite plan enhancements:


   * Lite plan now includes a dedicated read-only sample IBM COS storage associated to the Presto engine to support querying sample and benchmarking data.

   * You can now work with tpcds sample worksheets for high performance use cases and Gosales sample worksheet for Data engineering and GenAI use cases.

   * Query Optimizer is now automatically enabled for High Performance BI use cases.


## 29 October 2024 - Version 2.0.4
{: #lakehouse_29oct01}
{: release-note}

Engine and service enhancements

: This release includes the following engine and service enhancements:

   * The default value of the `task.max-drivers-per-task` property for Presto (Java) and Presto (C++) workers is now set based on the number of vCPUs.

   * You can enable the file pruning functionality in Query History Monitoring and Management (QHMM) from the **Query monitoring** page. You can also configure the maximum size and threshold percentage for the QHMM storage bucket. When the threshold is met during file upload or when a cleanup scheduler runs (default every 24 hours), older data is deleted. For more information, see [Configuring query monitoring](/docs/watsonxdata?topic=watsonxdata-qhmm#prn_qhmm).

   * Query History Monitoring and Management (QHMM) no longer stores the diagnostic data in the default IBM Managed trial bucket (`wxd-system`). To store the diagnostic data, you must now use a storage type supported for QHMM. For more information about using your own storage, see [Configuring query monitoring](/docs/watsonxdata?topic=watsonxdata-qhmm#cnsl_qhmm).

   * You can now verify query optimization status by checking the `wxdQueryOptimized` parameter in the JSON file. For more information, see [Running queries from the Presto (C++) CLI or Query workspace](/docs/watsonxdata?topic=watsonxdata-exec_inspect_optimizer).

Data sources enhancements

: This release includes the following data sources and storage enhancements:

   * Test connection feature is now available for the following data sources:
      * Apache Pinot
      * Cassandra
      * Prometheus


   * New data source **SAP HANA** is now available. You can use **Driver manager** under the **Configurations** page to manage drivers for SAP HANA data source. Each of these drivers undergoes a series of validations. For more information on SAP HANA data source and BYOJ process, see [SAP HANA](/docs/watsonxdata?topic=watsonxdata-saphana_conn).

Lite plan

: To enhance usability, the system catalogs (cmx and system) are now hidden for Lite plan users. The Lite plan instance with Presto (C++) engine includes `tpch` as the benchmarking catalog and the instance with Presto (Java) engine include `tpch` and `tpcds` as the benchmarking catalogs.

Deprecated features

: The following features are deprecated in this release:

   * The REST API feature to capture DDL changes in {{site.data.keyword.lakehouse_short}} through event listener is deprecated in this release and will be removed from {{site.data.keyword.lakehouse_short}} with version 2.1 release.

   * Support for Apache Spark 3.3 runtime is deprecated. You must upgrade to Spark 3.4. To update the Apache Spark version, see [Editing the Spark engine details](/docs/watsonxdata?topic=watsonxdata-view-end#edit-dtls).

## 25 September 2024 - Version 2.0.3
{: #lakehouse_25Sep01}

Data sources and storage enhancements

: This release includes the following new data sources and storage enhancements:

   * You can now enable Azure Data Lake Storage Gen1 Blob and Google Cloud Storage for Milvus. For more information, see [ADLS Gen1 Blob](/docs/watsonxdata?topic=watsonxdata-adls_genblob_storage) and [Google Cloud Storage](/docs/watsonxdata?topic=watsonxdata-gcs_storage).

   * You can create or add a new data source to the engine without attaching a catalog to it. A catalog can be attached to the data source at a later stage.

   * You can now use Apache Ozone storage for the Presto (Java) engine. For more information, see [Apache Ozone](/docs/watsonxdata?topic=watsonxdata-ozone_storage).

   * You can now configure the Apache Kafka data source to use the Salted Challenge Response Authentication Mechanism (SCRAM) authentication mechanism. You can upload a self-signed certificate. For more information, see [Apache Kafka](/docs/watsonxdata?topic=watsonxdata-kafka_database).

Integration enhancements

: This release of {{site.data.keyword.lakehouse_short}} introduces the following new or enhanced integrations with other services:

   * You can now integrate {{site.data.keyword.lakehouse_short}} with data build tool (dbt) for Spark engine for in-place data transformation within {{site.data.keyword.lakehouse_short}}. For more information, see [About dbt integration](/docs/watsonxdata?topic=watsonxdata-abt_dbt).

   * You can integrate {{site.data.keyword.lakehouse_short}} with Databand. This integration can enhance the monitoring capabilities by providing insights that extend beyond Spark UI and Spark History. For more information, see [Monitoring Spark application runs by using Databand](/docs/watsonxdata?topic=watsonxdata-mntr_dband).

   * You can integrate {{site.data.keyword.lakehouse_short}} with the following Business Intelligence (BI) visualization tools to access the connected data sources and build compelling and interactive data visualizations:

      * Tableau
      * Looker
      * Domo
      * Qlik
      * PowerBI

      For more information, see [About BI visualization tools](/docs/watsonxdata?topic=watsonxdata-abt_bi).

Engine and service enhancements

: This release of {{site.data.keyword.lakehouse_short}} introduces the following engine and service enhancements:

   * Iceberg tables are supported by Query Optimizer. For more information, see [Query Optimizer](/docs/watsonxdata?topic=watsonxdata-about_optimizer).

   * You can now use the data build tool (dbt-watsonx-presto) adapter to build, test, and document data models for the Presto (Java) engine. For more information, see [dbt-watsonx-presto](/docs/watsonxdata?topic=watsonxdata-dbt_watsonx_presto).

   * A new customization property (file-column-names-read-as-lower-case) is now available for Presto (C++) engine to avoid upper case and lower case mismatch in columns names. For more information, see [Catalog properties for Presto (C++)](/docs/watsonxdata?topic=watsonxdata-api_custom_pcpp_ctg).


Access management enhancements

: This release of {{site.data.keyword.lakehouse_short}} introduces the following access management enhancements:

   * You can now add users and user groups to define data policy rules. For more information, see [Data policy](/docs/watsonxdata?topic=watsonxdata-data_policy).

   * Administrators can now select TPCDS and TPCH catalogs to create access control policies. ‘Select’ is the only allowed operation to define rules with these catalogs. To define data policies, see [Data policy](/docs/watsonxdata?topic=watsonxdata-data_policy).

   * Administrators can now edit resource group configuration after creating the resource group. For more information, see [Configuring Presto resource groups](/docs/watsonxdata?topic=watsonxdata-conf_rcrs_grp).

IBM Knowledge Catalog governance policies for data sources
: You can now apply IBM Knowledge Catalog governance policies to the following data sources in Presto:

   * Oracle
   * PostgreSQL
   * MySQL
   * SQL Server
   * Db2

Ingestion enhancements
: This release of {{site.data.keyword.lakehouse_short}} includes the following improvements to the ingestion workflow:

   * You can now submit an ingestion job using the data sources. For more information, see [Ingesting data by using Spark through the web console](/docs/watsonxdata?topic=watsonxdata-ingest_spark_ui).

   * You can now ingest data using AVRO, and ORC file formats. For more information, see [About data ingestion](/docs/watsonxdata?topic=watsonxdata-load_ingest_data).

   * You can preview uploaded files and click table headers to edit column names. For more information, see [Ingesting data by using Spark through the web console](/docs/watsonxdata?topic=watsonxdata-ingest_spark_ui).

   * You can access and view Spark logs associated with an ingestion job. For more information, see [Accessing Spark logs for ingestion jobs](/docs/watsonxdata?topic=watsonxdata-ingest_sparklogshistory).

Lite plan

: You can provision your Lite plan instance based on the following three use cases. Select one use case from the list to proceed:

   * Generative AI : You can explore Generative AI use cases using this option. The provisioned instance includes Presto, Milvus, and Spark.
   * High Performance BI : You can explore BI visualization functionalities using this option. The provisioned instance includes Presto (C++) and Spark.
   * Data Engineering Workloads : You can use data engineering workload to explore various workload driven use cases. The provisioned instance includes Presto (Java) and Spark.

   For more information, see [Lite plan](/docs/watsonxdata?topic=watsonxdata-tutorial_prov_lite_1).

## 27 August 2024 - Version 2.0.2
{: #lakehouse_28Aug032024}


**Data sources and storage enhancements**
{: #28Aug_1_2024}

This release includes the following new data sources and storage enhancements:

* Content Aware Storage (CAS) is now called Data Access Service (DAS).

* Apache Hive is upgraded to version 4.0.0.

* You can now view the DAS endpoint from the **Storage details** page. For more information, see [Exploring storage objects](/docs/watsonxdata?topic=watsonxdata-buck-obj).

**Integration enhancements**
{: #28Aug_2_2024}

This release of {{site.data.keyword.lakehouse_short}} introduces the following new or enhanced integrations with other services:

* You can now use the governance capabilities of IBM Knowledge Catalog for SQL views within the {{site.data.keyword.lakehouse_short}} platform. For more information, see [Integrating with IBM Knowledge Catalog (IKC)](/docs/watsonxdata?topic=watsonxdata-ikc_integration).

* IBM {{site.data.keyword.lakehouse_short}} now supports Apache Ranger policies to govern data with Presto (C++) engines. For more information, see [Apache Ranger policy](/docs/watsonxdata?topic=watsonxdata-ranger_1).


**Engine and service enhancements**
{: #28Aug_3_2024}

This release of {{site.data.keyword.lakehouse_short}} introduces the following engine and service enhancements:

* Instance administrators can now configure resource groups in Presto. For more information, see [Resource groups](/docs/watsonxdata?topic=watsonxdata-rg_ov).

* You can now use an API to execute queries and retrieve results. For more information, see [API](https://cloud.ibm.com/apidocs/watsonxdata#create-execute-query){: external}.

* You can now configure or change the log level of Presto (Java) through API customization. For more information, [API](https://cloud.ibm.com/apidocs/watsonxdata#update-presto-engine){: external}.

* You can now generate Number of Distinct Values (NDV) column statistics with the Iceberg Spark Analyze procedure to enhance the Spark Cost-Based Optimizer (CBO) for improved query planning.

* You can now use the custom data source option to connect to Black Hole and Local File connectors for the Presto (Java) engine. For more information, see [Custom data source](/docs/watsonxdata?topic=watsonxdata-custom_database).

* You can now generate JSON snippet for Presto engine and Milvus service. You can copy/paste it over to the {{site.data.keyword.lakehouse_short}} Presto and Milvus connector UI in IBM Cloud Pak for Data and watsonx to simplify the connection creation. For more information, see [Getting connection information](/docs/watsonxdata?topic=watsonxdata-get_connection).


**Access management enhancements**
{: #28Aug_4_2024}

This release of {{site.data.keyword.lakehouse_short}} introduces the following access management enhancements:

* You can now control access to Presto (C++) engines. For more information, see [Engine (Presto (Java) or Presto (C++))](/docs/watsonxdata?topic=watsonxdata-role_priv#engine_presto).

* You can now grant component access to users and user groups in batch. For more information, see [Managing user access](/docs/watsonxdata?topic=watsonxdata-manage_access).

* You can now have System Access Control (SAC) plug-in logs with DEBUG information in Presto. For more information, see [API customization](/docs/watsonxdata?topic=watsonxdata-api_custom_ov).

**Ingestion enhancements**
{: #28Aug_5_2024}

This release of {{site.data.keyword.lakehouse_short}} introduces the following ingestion enhancements:

* Ingestion workflow in {{site.data.keyword.lakehouse_short}} is now simplified to submit an ingestion job, and support local file ingestion. For more information, see [Ingesting data by using Spark through the web console](/docs/watsonxdata?topic=watsonxdata-ingest_spark_ui).
* You can now ingest data using JSON file format. For more information, see [About data ingestion](/docs/watsonxdata?topic=watsonxdata-load_ingest_data).
* CSV file properties are now available as parameters supporting `ibm-lh data-copy`. For more information, see [Options and parameters supported in ibm-lh tool](/docs/watsonxdata?topic=watsonxdata-cli_commands).
* New environment variables are available for Spark ingestion through `ibm-lh tool` command line. For more information, see [Spark ingestion through ibm-lh tool command line](/docs/watsonxdata?topic=watsonxdata-ingest_spark_cli).


## 01 August 2024 - Version 2.0.1
{: #lakehouse_31July032024}

**Data sources**
{: #31JULY_1_2024}

* You can now connect to Db2 data sources by using IBM API key as the authentication mechanism. For more information, see [IBM Db2](/docs/watsonxdata?topic=watsonxdata-db2_database).
* Presto (C++) engine can now be associated with Arrow Flight service data sources. Read only operations are supported. The following Arrow Flight service data sources are supported:
     * Salesforce
     * MariaDB
     * Greenplum
     * Apache Derby

For more information, see [Arrow Flight service](/docs/watsonxdata?topic=watsonxdata-arrow_database){: external}.

* The following new databases are available for Presto (Java) engine:
     * Redis
     * Apache Druid
     * For more information, see [Redis](/docs/watsonxdata?topic=watsonxdata-redis_database){: external} and [Apache Druid](/docs/watsonxdata?topic=watsonxdata-druid_database){: external}.

**Integrations**
{: #31JULY_2_2024}

* When integrating IBM Knowledge Catalog with IBM {{site.data.keyword.lakehouse_short}}, you can configure data protection rules for individual rows in a table, allowing users to access a subset of rows in a table. For more information, see [Filtering rows](https://dataplatform.cloud.ibm.com/docs/content/wsj/governance/filter-rows.html?context=cpdaas&audience=wdp){: external}.
* You can now apply the following Apache Ranger policies for Presto (Java) engines:
     * Row-level filtering: Users can access a subset of rows in a table. For more information, see [Adding row-level filtering policy](/docs/watsonxdata?topic=watsonxdata-row_ranger){: external}.
     * Column masking: Restrict users to seeing masked values instead of displaying sensitive data. For more information, see [Adding column masking policy](/docs/watsonxdata?topic=watsonxdata-colmn_ranger_1){: external}.

* You can now integrate IBM {{site.data.keyword.lakehouse_short}} with on-premises IBM DataStage. You can use DataStage service to load and to read data from IBM {{site.data.keyword.lakehouse_short}}. For more information, [Integrating with DataStage](/docs/watsonxdata?topic=watsonxdata-dc_integration){: external}.

**Authentication and authorization**
{: #31JULY_3_2024}

* The Spark access control extension allows additional authorization, enhancing security at the time of application submission. If you enable the extension in the spark configuration, only authorized users are allowed to access and operate IBM {{site.data.keyword.lakehouse_short}} catalogs through Spark jobs. For more information, see [Enhancing Spark application submission using Spark access control extension](/docs/watsonxdata?topic=watsonxdata-spark-extnsn){: external}.

* IBM {{site.data.keyword.lakehouse_short}} now supports object storage proxy and signature for Azure Data Lake Storage and Azure Blob Storage. For more information, see [Using DAS proxy to access ADLS and ABS compatible buckets](/docs/watsonxdata?topic=watsonxdata-cas_proxy_adls){: external}.

* Lightweight Directory Access Protocol (LDAP) is now provided for Teradata and Db2 data sources. The user needs to set up this configuration at the server level. For Teradata, explicitly choose the authentication mechanism type as LDAP in the UI. For more information, [Teradata](/docs/watsonxdata?topic=watsonxdata-teradata_database){: external}.

DAS proxy to access ADLS and ABS buckets and LDAP enhancements are Tech preview in version 2.0.1.
{: note}

* Milvus now supports partition-level isolation for users. Administrators can authorize specific user actions on partitions. For more information, see [Service (Milvus)](/docs/watsonxdata?topic=watsonxdata-role_priv#milvus){: external}.

**Storage**
{: #31JULY_4_2024}

* You can now add the following storage to Presto (Java) engine in IBM {{site.data.keyword.lakehouse_short}}:
     * Azure Data Lake Storage Gen2
     * Azure Data Lake Storage Gen1 Blob

For more information, see [Azure Data Lake Storage Gen2](/docs/watsonxdata?topic=watsonxdata-reg_bucket#gen) and [Azure Data Lake Storage Gen1 Blob](/docs/watsonxdata?topic=watsonxdata-reg_bucket){: external}.

* You can modify the access key and secret key of a user-registered bucket for a storage. This feature is not applicable to default buckets, ADLS, or Google Cloud Storage. This feature can only be used if the new credentials successfully pass the test connection.

**Engines**
{: #31JULY_5_2024}

* You can now use the ALTER TABLE ADD, DROP, and RENAME column statements for MongoDB data source.
* You can now configure how Presto handles unsupported data types. For more information, see [ignore-unsupported-datatypes](/docs/watsonxdata?topic=watsonxdata-api_custom_ctg_pjcw&q=catalog&tags=watsonxdata#ignore){: external}.

**Catalogs**
{: #31JULY_6_2024}

* You can now associate and disassociate catalogs to an engine in bulk through UI under Manage associations in the Infrastructure manager page.

**API Customization and properties**
{: #31JULY_7_2024}

* The following customization parameters are added for Presto (C++) workers:

     * system-mem-limit-gb
     * system-mem-shrink-gb
     * system-mem-pushback-enabled

   For more information, see [Configuration properties for Presto (C++) - worker nodes](/docs/watsonxdata?topic=watsonxdata-api_custom_wkr_pcpp){: external}.

* The configuration property `optimizer.size-based-join-flipping-enabled` is added for Presto (C++) coordinator nodes. For more information, see [Configuration properties for Presto (C++) - coordinator nodes](/docs/watsonxdata?topic=watsonxdata-aapi_custom_pcpp_cood){: external}.

* Enhanced API customization to support data cache and fragment result cache for performance improvement.For more information, see [Configuration properties for Presto (Java) - coordinator and worker nodes](/docs/watsonxdata?topic=watsonxdata-api_custom_prm_pjcw){: external} and [Catalog properties for Presto (Java)](/docs/watsonxdata?topic=watsonxdata-api_custom_ctg_pjcw){: external}.

**Infrastructure manager**
{: #31JULY_9_2024}

* You can use search feature for the following values on the Infrastructure manager page:
     * database name
     * registered hostname
     * created by username
* You can now use the ‘Do Not Disturb’ toggle switch in the Notifications section under the bell icon to enable or disable pop-up notifications.
* You can find the connectivity information under the Connect information tile in the Configurations page. This information can be copied and downloaded to a JSON snippet.

**Query Workspace**
{: #31JULY_10_2024}

* You can run queries on all tables under a schema through the SQL query workspace without specifying the path `<catalog>.<schema>` by selecting the required catalogs and schemas from the new drop down list. For more information, [Running SQL queries](/docs/watsonxdata?topic=watsonxdata-run_sql){: external}.

**watsonx.data pricing plans**
{: #31JULY_11_2024}

* You can now delete the existing Lite plan instance before reaching the account cap limit of 2000 RUs, and create a new instance and consume the remaining resource units available in the account. For more information, see [watsonx.data Lite plan](/docs/watsonxdata?topic=watsonxdata-tutorial_prov_lite_1){: external}.


## 03 July 2024 - Version 2.0.0
{: #lakehouse_July032024}

**New data types for data sources**
{: #JULY_01_2024}

The following new data types are now available for some data sources. You can access these data types on the **Data manager** page under the **Add column** option.

* **BLOB**

     * Db2
     * Teradata
     * Oracle
     * MySQL
     * SingleStore

* **CLOB**

     * Db2
     * Teradata
     * Oracle

* **BINARY**

     * SQL Server
     * MySQL

Because the numeric data type is not supported in watsonx.data, you can use the decimal data type as an equivalent alternative to the numeric data type for Netezza data source.

You can now use the BLOB and CLOB data types with the SELECT statement in the Query workspace to build and run queries against your data for Oracle and SingleStore data sources.

You can now use the BLOB and CLOB data types for MySQL and PostgreSQL data sources as equivalents to LONGTEXT, BYTEA, and TEXT because these data types are not compatible with Presto (Java). These data types are mapped to CLOB and BLOB in Presto (Java) if data sources have existing tables with LONGTEXT, TEXT, and BYTEA data types.

* MySQL (CLOB as equivalent to LONGTEXT)
* PostgreSQL (CLOB as equivalent to TEXT)
* PostgreSQL (BLOB as equivalent to BYTEA)
* Netezza (decimal as equivalent to numeric)
* Oracle (BLOB and CLOB with the SELECT statement)
* SingleStore (BLOB and CLOB with the SELECT statement)

**New operations for Db2 data source**
{: #JULY_02_2024}

You can perform the following operations for BLOB and CLOB data types for Db2 data source:
* INSERT
* CREATE
* CTAS
* ALTER
* DROP

**New Arrow Flight service based data sources**
{: #JULY_03_2024}

You can now use the following data sources with Arrow Flight service:

* Greenplum
* Salesforce
* MariaDB
* Apache Derby

For more information, see [Arrow Flight service](/docs/watsonxdata?topic=watsonxdata-arrow_database){: external}.

**New data sources**
{: #JULY_04_2024}

You can now use the following data sources:

* Cassandra
* BigQuery
* ClickHouse
* Apache Pinot

For more information, see [Adding a database-catalog pair](/docs/watsonxdata?topic=watsonxdata-reg_database){: external}.

**Command to retrieve ingestion history**
{: #JULY_05_2024}

You can now retrieve the status of all ingestion jobs that are submitted by using the ibm-lh get-status --all-jobs CLI command. You can retrieve the status of all ingestion jobs that are submitted. You get the history records that you have access to.
For more information, see [Options and parameters supported in ibm-lh tool](/docs/watsonxdata?topic=watsonxdata-cli_commands){: external}.


**Additional roles for IBM Knowledge Catalog (IKC) S2S authorization**
{: #JULY_06_2024}

Besides data access, IBM Knowledge Catalog S2S authorization needs metadata access and Console API access to integrate with watsonx.data. The following new roles are created for IKC service access configuration:

* Viewer
* Metastore viewer

**Apache Ranger policies**
{: #JULY_07_2024}

IBM watsonx.data now supports Apache Ranger policies to allow integration with Presto engines.
For more information, see [Apache Ranger policy](/docs/watsonxdata?topic=watsonxdata-ranger_1){: external}.


**Version upgrade**
{: #JULY_08_2024}

* Presto (Java) engine is now upgraded to version 0.286.
* Milvus service is now upgraded to version to 2.4.0. Important features include:
     * Better Performance (Low Memory Utilisation)
     * Support Sparse Data
     * Inbuilt SPLADE Engine for Sparse Vector Embedding
     * BGE M3 Hybrid (Dense+Sparse) Search

**Hive Metastore (HMS) access in watsonx.data**
{: #JULY_09_2024}

You can now fetch metadata information for Hive Metastore by using REST APIs instead of getting the information from the engine details. HMS details are used by external entities to integrate with watsonx.data. You must have an Admin, Metastore Admin, or Metastore Viewer role to run the API.


**Semantic automation for data enrichment**
{: #JULY_10_2024}

Semantic automation for data enrichment leverages generative AI with IBM Knowledge Catalog to understand your data on a deeper level and enhance data with automated enrichment to make it valuable for analysis. Semantic layer integration is available for Lite plan users only as a 30 days trial version.
For more information, see [Semantic automation for data enrichment in watsonx.data](/docs/watsonxdata?topic=watsonxdata-sal_title).


**Query Optimizer to improve query performance**
{: #JULY_11_2024}

You can now use Query Optimizer, to improve the performance of queries that are processed by the Presto (C++) engine. If Query Optimizer determines that optimization is feasible, the query undergoes rewriting; otherwise, the native engine optimization takes precedence.
For more information, see [Query Optimizer overview](/docs/watsonxdata?topic=watsonxdata-about_optimizer).



**New name for Presto engine in watsonx.data**
{: #JULY_12_2024}

Presto is renamed to Presto (Java).


**New engine (Presto C++) in watsonx.data**
{: #JULY_13_2024}

You can provision a Presto (C++) engine ( version 0.286) in watsonx.data to run SQL queries on your data source and fetch the queried data.
For more information, see Presto (C++) overview.

**Using proxy to access S3 and S3 compatible buckets**
{: #JULY_14_2024}

External applications and query engines can access the S3 and S3 compatible buckets managed by watsonx.data through an S3 proxy.
For more information, see [Using S3 proxy to access S3 and S3 compatible buckets](/docs/watsonxdata?topic=watsonxdata-cas_proxy).

**Mixed case feature flag for Presto (Java) engine**
{: #JULY_16_2024}

The mixed case feature flag, which allows to switch between case sensitive and case insensitive behavior in Presto (Java), is available. The flag is set to OFF by default and can be set to ON during the deployment of watsonx.data.
For more information, see [Presto (Java) mixed-case support overview](/docs/watsonxdata?topic=watsonxdata-mixed_case_overview).

**New storage type Google Cloud Storage**
{: #JULY_17_2024}

You can now use new storage type Google Cloud Storage. For more information, see [Adding storage-catalog pair](/docs/watsonxdata?topic=watsonxdata-reg_bucket#gcs).


## 31 May 2024 - Version 1.1.5
{: #lakehouse_May312024}

**Provision Spark engine in {{site.data.keyword.lakehouse_short}} Lite plan**
{: #MAY_01_2024}

You can now add a small-sized Spark engine (single node) in the {{site.data.keyword.lakehouse_short}} Lite plan instance. For more information, see [watsonx.data Lite plan](/docs/watsonxdata?topic=watsonxdata-tutorial_prov_lite_1).


**Updates related to Spark labs**
{: #MAY_02_2024}

* **Working with Jupyter Notebooks from Spark labs**

: You can now install the Jupyter extension from the VS Code Marketplace inside your Spark lab and work with Jupyter Notebooks. For more information, see [Create Jupyter Notebooks](/docs/watsonxdata?topic=watsonxdata-lab_nsp#dev_lab_02).

* **Accessing Spark UI from Spark labs**

You can now access the Spark user interface (UI) from Spark labs to monitor various aspects of running a Spark application. For more information, see [Accessing Spark UI from Spark labs](/docs/watsonxdata?topic=watsonxdata-lab_mon_nsp#lab_nsp-ui).

**New region to provision for IBM Cloud instance**
{: #MAY_03_2024}

You can now provision your IBM Cloud instance in the Sydney region.

## 30 Apr 2024 - Version 1.1.4
{: #lakehouse_Apr242024}


A new version of {{site.data.keyword.lakehouse_short}} was released in April 2024.

This release includes the following features and updates:

**Kerberos authentication for HDFS connections**
{: #APR_01_2024}

You can now enable Kerberos authentication for secure Apache Hadoop Distributed File System (HDFS) connections. For more information, see [HDFS](/docs/watsonxdata?topic=watsonxdata-reg_bucket#hdfs).

**New data sources**
{: #APR_02_2024}

The following new data sources are now available:
* Oracle
* Amazon Redshift
* Informix
* Prometheus

For more information, see [Data sources](/docs/watsonxdata?topic=watsonxdata-reg_database).

**Test SSL connections**
{: #APR_03_2024}

You can now test SSL connections for the MongoDB and SingleStore data sources.


**Uploading description files for Apache Kafka data source**
{: #APR_04_2024}

The Apache Kafka data source stores data as byte messages that producers and consumers must interpret. To query this data, consumers must first map it into columns. Now, you can upload topic description files that convert raw data into a table format. Each file must be a JSON file that contains a definition for a table. To upload these JSON files from the UI, go to the overview page of the Apache Kafka database that you registered and select the **Add topic** option. For more information, see [Apache Kafka](/docs/watsonxdata?topic=watsonxdata-reg_database#kafka).

**License plans for {{site.data.keyword.lakehouse_short}}**
{: #APR_05_2024}

{{site.data.keyword.lakehouse_full}} now offers the following license plans.

* Lite plan
* Enterprise plan

For more information about the different license plans, see [IBM® watsonx.data pricing plans](/docs/watsonxdata?topic=watsonxdata-getting-started).


**Presto (Java) engine version upgrade**
{: #APR_06_2024}

The Presto (Java) engine is now upgraded to version 0.285.1.

**Pause or resume Milvus**
{: #APR_07_2024}

You can now pause or resume Milvus service. Pausing your service can avoid incurring charges.


**Spark is now available as a native engine**
{: #APR_08_2024}

In addition to registering external Spark engines, you can now provision native Spark engine on your IBM watsonx.data instance. With native Spark engine, you can fully manage Spark Engine configuration, manage access to Spark Engines and view applications by using watsonx.data UI and REST API endpoints. For more information, see [Provisioning Native Spark engine](/docs/watsonxdata?topic=watsonxdata-prov_nspark).

**Ingest data using native Spark Engines**
{: #APR_09_2024}

You can now submit ingestion jobs using native Spark Engines. For more information, see [Working with different table formats](/docs/watsonxdata?topic=watsonxdata-hudi_nsp).

## 27 Mar 2024 - Version 1.1.3
{: #lakehouse_Mar272024}


A new version of {{site.data.keyword.lakehouse_short}} was released in March 2024.

This release includes the following features and updates:


**New data type for some data sources**
{: #mar_01_2024}

You can now use the BINARY data type  with the SELECT statement in the Query workspace to build and run queries against your data for the following data sources:

* Elasticsearch
* SQL Server
* MySQL

New data types: BLOB and CLOB are available for MySQL, PostgreSQL, Snowflake, SQL Server, and Db2 data sources. You can use these data types only with SELECT statements in the Query workspace to build and run queries against your data.



**Delete data by using the DELETE FROM feature for Iceberg data sources**
{: #mar_02_2024}

You can now delete data from tables in Iceberg data sources by using the DELETE FROM feature.

You can specify the table property delete mode for new tables by using either copy-on-write mode or merge-on-read mode (default). For more information, see [SQL statements](/docs/watsonxdata?topic=watsonxdata-supported_sql_statements).



**ALTER VIEW statement for Iceberg data source**
{: #mar_03_2024}

You can now use the following SQL statement in the Query workspace to build and run queries against your data for ALTER VIEW:

ALTER VIEW name RENAME TO new_name



**Upload SSL certificates for Netezza Performance Server data sources**
{: #mar_03_2024}

You can now browse and upload the SSL certificate for SSL connections in Netezza Performance Server data sources. The valid file formats for SSL certificate are .pem, .crt, and .cer. You can upload SSL certificates by using the Adding a database-catalog pair option in the Infrastructure manager.



**Query data from Db2 and Watson Query**
{: #mar_04_2024}

You can now query nicknames that are created in Db2 and virtualized tables from  Watson Query instances.



**SSL connection for IBM Data Virtualization Manager for z/OS data source**
{: #mar_05_2024}

You can now enable SSL connection for the IBM Data Virtualization Manager for z/OS data source by using the Add database user interface to secure and encrypt the database connection. Select Validate certificate to validate whether the SSL certificate that is returned by the host is trusted. You can choose to provide the hostname in the SSL certificate.



**Use data from Apache Hudi catalog**
{: #mar_05_2024}

You can now connect to and use data from Apache Hudi catalog.



**Add Milvus as a service in {{site.data.keyword.lakehouse_short}}**
{: #mar_06_2024}

You can now provision Milvus as a service in {{site.data.keyword.lakehouse_short}} with the following features:

* Provision different storage variants such as starter, medium, and large nodes.

* Assign Admin or User roles for Milvus users: User access policy is now available for Milvus users. Using the Access Control UI, you can assign Admin or User roles for Milvus users and also grant, revoke, or update the privilege. 

* Configure the Object storage for Milvus to store data. You can add or configure a custom bucket and specify the username, password, region, and bucket URL.

For more information, see [Milvus](/docs/watsonxdata?topic=watsonxdata-adding-milvus-service).


**Load data in batch by using the ibm-lh ingestion tool**
{: #mar_07_2024}

You can now use the ibm-lh ingestion tool to run batch ingestion procedures in non-interactive mode (from outside the ibm-lh-tools container), by using the ibm-lh-client package. For more information, see [ibm-lh commands and usage](https://www.ibm.com/docs/SSDZ38_1.1.x/wxd-client/topics/ibm_lh_commands.html).

 

**Creating schema by using bulk ingestion in web console**
{: #mar_08_2024}

You can now create a schema by using the bulk ingestion process in the web console, if the schema is not previously created.



**Use time-travel queries in Apache Iceberg tables**
{: #mar_09_2024}

You can now run the following time-travel queries by using branches and tags in Apache Iceberg table snapshots:

- SELECT *FROM `<table name>` FOR VERSION AS OF 'historical-tag'

- SELECT *FROM `<table name>` FOR VERSION AS OF 'test-branch'




**Access Cloud Object Storage without credentials**
You can now access your Cloud Object Storage bucket without credentials, by using the Data Access Service (DAS) endpoint. For more information about getting DAS endpoint, see [Getting DAS endpoint](/docs/watsonxdata?topic=watsonxdata-cas_ep).




## 28 Feb 2024 - Version 1.1.2
{: #lakehouse_Feb282024}


A new version of {{site.data.keyword.lakehouse_short}} was released in February 2024.

This release includes the following features and updates:

**SSL connection for data sources**
{: #feb_01_2024}

You can now enable SSL connection for the following data sources by using the **Add database** user interface to secure and encrypt the database connection.  :

* Db2

* PostgreSQL

For more information, see [Adding a database](/docs/watsonxdata?topic=watsonxdata-reg_database).



**Secure ingestion job history**
{: #feb_02_2024}

Now, users can view only their own ingestion job history. Administrators can view the ingestion job history for all users.




**SQL enhancements**
{: #feb_03_2024}

You can now use the following SQL statements in the Query workspace to build and run queries against your data:

   * Apache Iceberg data sources
        - CREATE VIEW
        - DROP VIEW
   * MongoDB data sources
        - DELETE




**New data types BLOB and CLOB for Teradata data source**
{: #feb_04_2024}

New data types BLOB and CLOB are available for Teradata data source. You can use these data types only with SELECT statements in the Query workspace to build and run queries against your data.




**Create a new table during data ingestion**
{: #feb_06_2024}

Previously, you had to have a target table in {{site.data.keyword.lakehouse_short}} for ingesting data. Now, you can create a new table directly from the source data file (available in parquet or CSV format) by using data ingestion from the **Data Manager**. You can create the table by using the following methods of ingestion:

* Ingesting data by using Iceberg copy loader.

* Ingesting data by using Spark.




**Perform ALTER TABLE operations on a column**
{: #feb_07_2024}

With an Iceberg data source, you can now perform ALTER TABLE operations on a column for the following data type conversions:

* int to bigint

* float to double

* decimal (num1, dec_digits) to decimal (num2, dec_digits), where num2>num1.



**Better query performance by using sorted files**
{: #feb_09_2024}

With an Apache Iceberg data source, you can generate sorted files, which reduce the query result latency and improve the performance of Presto (Java). Data in the Iceberg table is sorted during the writing process within each file. 

You can configure the order to sort the data by using the `sorted_by` table property. When you create the table, specify an array of one or more columns involved in sorting. To disable the feature, set the session property `sorted_writing_enabled` to false. 



## 31 Jan 2024 - Version 1.1.1
{: #lakehouse_Jan312024}


A new version of {{site.data.keyword.lakehouse_short}} was released in January 2024.

This release includes the following features and updates:

**IBM Data Virtualization Manager for z/OS® connector**
{: #wn_01_2024}

You can now use the new IBM Data Virtualization Manager for z/OS® connector to read and write IBM Z® without moving, replicating, or transforming the data. For more information, see [Connecting to an IBM Data Virtualization Manager (DVM) data source](https://www.ibm.com/docs/en/iis/11.7?topic=analyzer-connecting-data-virtualization-manager-dvm-data-source).

**Teradata connector is enabled for multiple `ALTER TABLE` statements**
{: #wn_03_2024}

Teradata connector now supports the `ALTER TABLE RENAME TO`, `ALTER TABLE DROP COLUMN`, and `ALTER TABLE RENAME COLUMN column_name TO new_column_name` statements.

**Support for time travel queries**
{: #wn_05_2024}

Iceberg connector for Presto (Java) now supports time travel queries.

**The property `format_version` now shows the current version**
{: #wn_06_2024}

The property `format_version` now shows the correct value (current version) when you create an Iceberg table.


## 29 Nov 2023 - Version 1.1.0
{: #lakehouse_Nov292023}

A new version of {{site.data.keyword.lakehouse_short}} was released in November 2023.

This release includes the following features and updates:

**Presto (Java) case-sensitive behavior**
{: #wn_00}

The Presto (Java) behavior is changed from case-insensitive to case-sensitive. Now you can provide the object names in the original case format as in the database. For more information, see [Case-sensitive search configuration with Presto (Java)](/docs/watsonxdata?topic=watsonxdata-ts_cs).

**Roll-back feature**
{: #wn_01}

You can use the Rollback feature to rollback or rollforward to any snapshots for Iceberg tables.



**Capture Data Definition Language (DDL) changes**
{: #wn_04}

You can now capture and track the DDL changes in {{site.data.keyword.lakehouse_short}} by using an event listener.
For more information, see [Capturing DDL changes](/docs/watsonxdata?topic=watsonxdata-dll_changes).

**Ingest data by using Spark**
{: #wn_05}

You can now use the IBM Analytics Engine that is powered by Apache Spark to run ingestion jobs in {{site.data.keyword.lakehouse_short}}.

For more information, see [Ingesting data by using Spark](/docs/watsonxdata?topic=watsonxdata-ingest_spark_ui).

**Integration with Db2 and Netezza Performance Server**
{: #wn_06}

You can now register Db2 or Netezza Performance Server engines in {{site.data.keyword.lakehouse_short}} console.

For more information, see [Registering an engine](/docs/watsonxdata?topic=watsonxdata-reg_engine).

**New connectors**
{: #wn_07}

You can now use connectors in {{site.data.keyword.lakehouse_short}} to establish connections to the following types of databases:

- Teradata
- Delta Lake
- Elasticsearch
- SingleStoreDB
- Snowflake

For more information, see [Adding a database](/docs/watsonxdata?topic=watsonxdata-reg_database).

**AWS EMR for Spark**
{: #wn_08}

You can now run Spark applications from Amazon Web Services Elastic MapReduce (AWS EMR) to achieve the {{site.data.keyword.lakehouse_short}} Spark use cases:

- Data ingestion
- Data querying
- Table maintenance

For more information, see [Using AWS EMR for Spark use case](/docs/watsonxdata?topic=watsonxdata-spark-emr).

## 7 July 2023 - Version 1.0.0
{: #lakehouse_july72023}

{{site.data.keyword.lakehouse_short}} is a new open architecture that combines the elements of the data warehouse and data lake models. The best-in-class features and optimizations available on the {{site.data.keyword.lakehouse_short}} make it an optimal choice for next generation data analytics and automation. In the first release ({{site.data.keyword.lakehouse_short}} 1.0.0), the following features are supported:

- Creating, scaling, pausing, resuming, and deleting the Presto (Java) query engine
- Associating and dissociating a catalog with an engine
- Exploring catalog objects
- Adding and deleting a database-catalog pair
- Updating database credentials
- Adding and deleting bucket-catalog pair
- Exploring bucket objects
- Loading data
- Exploring data
- Querying data
- Query history
