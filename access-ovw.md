---

copyright:
  years: 2022, 2025
lastupdated: "2025-02-21"

keywords: access, access control, access management

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

# Access management and governance in {{site.data.keyword.lakehouse_short}}
{: #access_mgt}

This topic provides details about access management and governance in {{site.data.keyword.lakehouse_short}}.
{: shortdesc}

Access management is a critical aspect of security that ensures only authorized individuals can access {{site.data.keyword.lakehouse_short}} and also involves defining right access and privileges to right people to right components and services in {{site.data.keyword.lakehouse_short}}.

Access management in {{site.data.keyword.lakehouse_short}} includes three levels of access control:

* User authentication (Level 1)
* User access to resources (Level 2)
* User access to data (Level 3)


## Level 1 authentication in {{site.data.keyword.lakehouse_short}} on IBM Cloud and AWS
{: #level1}

User authentication is the first-level access required for users to authenticate into the {{site.data.keyword.lakehouse_short}}. It has two parts to it.

* Access to the platform where {{site.data.keyword.lakehouse_short}} is deployed. For example, {{site.data.keyword.lakehouse_short}} on IBM cloud, AWS. For more information, see [Managing users](https://cloud.ibm.com/docs/account?topic=account-iamuserinv&interface=ui).
* Role Based Access Control within {{site.data.keyword.lakehouse_short}}. For example, Admin and User roles with specific access and privileges.For more information, see [Managing user roles](https://cloud.ibm.com/docs/account?topic=account-account-services&interface=ui#account-management-actions-role).


Level 1 authentication in watsonx.data on IBM Cloud is aligned with the IBM Cloud authentication framework. For more information, see [IBM Cloud IAM roles](https://cloud.ibm.com/docs/account?topic=account-userroles&interface=ui) and [Actions and roles for account management services](https://cloud.ibm.com/docs/account?topic=account-account-services&interface=ui#account-management-actions-role).



You can create access groups, or give access to a trusted profile, user, or service ID access to any of the target and specific permissions as depicted in the following illustration:



In addition to the authentication, in IBM cloud, the IAM platform roles are assigned some privileges and permissions by default. The following table provides the details. These roles are to be assigned to users or user groups.


| Field | Description |
|--------------------------|----------------|
|IAM platform roles	|Actions|
|IAM Platform Administrator| lakehouse.metastore.admin \n lakehouse.dashboard.view|
|IAM Platform Operator, Editor, Viewer	|lakehouse.dashboard.view|
|Others	|Depends on the actions that are assigned by the administrator|
|jdbc.url |	Provide the JDBC URL.|
{: caption="Platform Roles " caption-side="bottom"}


The following table provides the service role details that are specific to watsonx.data  on IBM Cloud and AWS. Metastore Admin role is used for Db2, Netezza, and Spark. Metastore Admin has full access to HMS Thrift API. Metastore Viewer role has read access to HMS Rest API. The Data Access role is used only for IKC integration on data profiling.

| Field | Description |
|--------------------------|----------------|
|Service roles	|Actions	|Permissions|
|Metastore Admin| lakehouse.metastore.admin	| Manage metastore data|
|Metastore Viewer	| lakehouse.metastore.view	|View metastore data|
|Data Access (primarily used for service to service integration. For example, IKC integration with WXD)	| lakehouse.data.access |	Access data|
{: caption="Service roles " caption-side="bottom"}



## Authentication options
{: #levelauth}


Users can authenticate by using IBM API key or IAM token for API or CLI access to watsonx.data API and services. Username and password to access watsonx.data UI console.

**Authentication options for presto-cli**
Users can also use presto-cli or connect to Presto via JDBC with IBM Cloud – IBM API key or IAM token. For more information, see [Connecting to Presto server in watsonx.data on IBM Cloud](https://cloud.ibm.com/docs/watsonxdata?topic=watsonxdata-con-presto-serv).


## User access to resources (Level 2)
{: #leve2}

With the second-level access control, you can assign roles for watsonx.data users to view, edit, and administer the resources, which include engines, catalogs, storage, and databases.

Controlling access to the engines and other components is a critical requirement for many enterprises. To ensure that the resource usage is under control, IBM® watsonx.data provides the ability to manage access controls on these resources. A user with admin privileges on the resources can grant access to other users.

For more information on L2 access control in watsonx.data on IBM Cloud and AWS, see [Managing users](https://cloud.ibm.com/docs/watsonxdata?topic=watsonxdata-manage_access) and [Managing roles and privileges](https://cloud.ibm.com/docs/watsonxdata?topic=watsonxdata-role_priv).


## Data access (Level 3)
{: #leve3}

At the data access level, you can define data access policies and grant or restrict access to schema, table, and columns in watsonx.data. You can define policies by using {{site.data.keyword.lakehouse_short}} Access Management System, or IBM Knowledge Catalog integration or Apache Ranger integration.



**{{site.data.keyword.lakehouse_short}} Access management system**
For more information about data access policies in watsonx.data on IBM Cloud, see [Managing data policy rules](https://cloud.ibm.com/docs/watsonxdata?topic=watsonxdata-data_policy).

**IBM Knowledge Catalog integration for data governance and access control**
Integrating watsonx.data with IBM Knowledge Catalog provides self-service access to data assets for knowledge workers who need to use those data assets to gain insights.

For more information, see [Integrating with IBM Knowledge Catalog](https://cloud.ibm.com/docs/watsonxdata?topic=watsonxdata-ikc_integration).

**Apache Ranger integration for data governance and access control**
IBM watsonx.data supports Apache Ranger policies to allow comprehensive data security on integrating with multiple governance tools and engines.

For more information, see [Enabling Apache Ranger policy for resources](https://cloud.ibm.com/docs/watsonxdata?topic=watsonxdata-ranger_1).



## Data Access Service (DAS)
{: #das_ams}

Data Access Service (DAS) proxy in watsonx.data provides a unified way to access object storage, govern external engines, and audit data access. All of these are accomplished without exposing credentials or requiring complex modifications to engines, which are not controlled by watsonx.data.

For more information, see [Data Access Service overview](https://cloud.ibm.com/docs/watsonxdata?topic=watsonxdata-cas_ep_ov).


## Getting connection information
{: #conn_in}

You can see the connection information of watsonx.data from the Connect information tile of the Configurations page and from the Instance details page. For more information about watsonx.data connections, see [Getting connection information](https://cloud.ibm.com/docs/watsonxdata?topic=watsonxdata-get_connection).
