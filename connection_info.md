---

copyright:
  years: 2022, 2025
lastupdated: "2024-08-01"

keywords: connection, watsonx.data

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

# Getting connection information
{: #get_connection}

You can now find the connectivity information for {{site.data.keyword.lakehouse_full}} in the **Connection information** tile in the **Configurations** page and in the **Instance details** page. You can copy JSON snippet and export JSON.

## Connection information
{: #get_connection_conninfo}

The **Connection information** tile in the **Configurations** page provides the following information:

   * **Instance details**:
   * Host IP address
   * Port
   * Instance CRN
   * SSL certificate
   * **Engine and service connection details**
   * Select the checkbox for **Generate JSON**
   * You can select one engine for the JSON snippet.

## BI tools
{: #get_connection_vscode}

From the **BI tools** tab, you can view the following details:

### Tableu
{: #get_connection_tableu}

Expand the Tableu section to see the following details:

* Server
* Port
* Catalog
* Username
* Password: Enter the API key for authentication.
* SSL certificate
* Copy TDS snippet
* Export TDS

Data source files are shortcuts to quickly connecting to the original data that you use often. Data source files does not include the actual data but the information necessary to connect to the actual data. For more information, see [Save Data Sources](https://help.tableau.com/current/pro/desktop/en-us/export_connection.htm).
{: note}


You can also click the link to view BI connection documentation.

### Power BI
{: #get_connection_powerbi}

Expand the Power BI section to see the following details:

* Server
* Port
* Catalog
* Username
* Password: Enter the API key for authentication.
* SSL certificate

You can also click the link to view BI connection documentation.

### Qlik
{: #get_connection_qlik}

Expand Qlik section to see the following details:

* Hostname
* Port
* Catalog
* Username
* Password: Enter the API key for authentication.
* SSL certificate

You can also click the link to view BI connection documentation.

### Domo
{: #get_connection_domo}

Expand the Domo section to see the following details:

* Server
* Port
* Database
* Username
* Password: Enter the API key for authentication.
* SSL certificate

You can also click the link to view BI connection documentation.

### Looker
{: #get_connection_looker}

Expand the Looker section to see the following details:

* Server
* Port
* Database
* Username
* Password: Enter the API key for authentication.
* SSL certificate

You can also click the link to view BI connection documentation.

## Visual Studio Code
{: #get_connection_vscode}

From the **Visual Studio Code** tab, you can view the following details:

### VS Code details
{: #get_connection_vscode_details}

Expand your VS Code to see the following details:

* Host IP address
* API key: Enter the API key for authentication.
* Username

### View VS Code connection configuration
{: #get_connection_vscode_conn}

Expand the VS Code connection configuration to view the following details:

* Connection information
* Export JSON snippet

## Data Build Tool (DBT)
{: #get_connection_dbt}

From the **Data Build Tool (DBT)** tab, you can view the following details:


### Presto engines
{: #get_connection_dbt_pst}

Expand your Presto engine to see the following details:

* Hostname
* Port
* Catalog: You can change the catalog by clicking the pencil icon.
* Username
* Password: Enter your platform API key here. For information about generating API key, see [Creating an API key in the console](https://cloud.ibm.com/docs/account?topic=account-userapikey&interface=ui#create_user_key).

You can copy the profile details by clicking **Copy profile snippet** or export the details as a `yaml` file by clicking **Export profile snippet**.

### Spark engines
{: #get_connection_dbt_spk}

Expand your Spark engine to see the following details:

* Spark engine endpoint
* Application endpoint
* Port

### Associated query servers
{: #get_connection_dbt_qs}

Expand the associated query server to view the following details:

* Hostname
* URI
* Catalog: You can change the catalog by clicking the pencil icon.
* Instance CRN
* Username
* API key: Enter your API key here. For information about generating API key, see [Creating an API key in the console](https://cloud.ibm.com/docs/account?topic=account-userapikey&interface=ui#create_user_key).

You can copy the profile details by clicking **Copy profile snippet** or export the details as a `yaml` file by clicking **Export profile snippet**.


## Instance details
{: #get_connection_inst}

The **Instance details** page provides the following details. To open the Instance details, click the i icon on the home page.

   * Region
   * Plan type
   * Cloud resource name (CRN)
   * Instance ID
   * Data Access Service (DAS) endpoint
   * Common Policy Gateway (CPG) endpoint
