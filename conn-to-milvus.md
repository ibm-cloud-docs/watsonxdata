---

copyright:
  years: 2022, 2024
lastupdated: "2025-02-26"

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

# Connecting to Milvus service
{: #conn-to-milvus}

Run any one of the following commands to connect with Milvus:
{: shortdesc}

## Before you begin
{: #prereq_conn_milvus}

Make sure that the following items are installed or available:

- Python and Pymilvus package. For more information, see [About PyMilvus](https://milvus.io/api-reference/pymilvus/v2.4.x/About.md).
- Hostname and port for the Milvus instance. You can get Milvus `host` and `port` information from **Infrastructure manager** (click the Milvus service to open the **Details** page and note the `host` and `port` information from the GRPC host).
- Assign a role to the user or [service ID](https://cloud.ibm.com/docs/account?topic=account-serviceids&interface=ui) from **Infrastructure manager**. For information about user roles, see [Managing roles and privileges]({{site.data.keyword.ref-role_priv-link}}#milvus){: external}.

## Procedure
{: #conn-to-milvusapikey}

You can connect to a Milvus service by using API key or IAM token.

1. Provision a Milvus service in {{site.data.keyword.lakehouse_short}}. For more information, see [Adding a Milvus service](watsonxdata?topic=watsonxdata-adding-milvus-service).
1. Run one of the following commands by using Python SDK (PyMilvus) to connect with Milvus for gRPC route:

     - Use one of the following commands to connect to Milvus using GRPC calls:

         ```bash
         print(fmt.format("start connecting to Milvus"))
         connections.connect(host="<host>", port="<port>", secure=True, user="ibmlhapikey", password="<api-key>")
         has = utility.has_collection("hello_milvus")
         print(f"Does collection hello_milvus exist in Milvus: {has}")
         ```
         {: codeblock}

        or

         ```bash
        from pymilvus import MilvusClient, DataType

        client = MilvusClient(
            host=<host>,
            port=<port>,
            secure=True,
            user="ibmlhapikey",
            password="<api-key>"
        )
         ```
         {: codeblock}

         Replace `<api-key>` with the IBM API key. For information about getting an API key, see [Getting IBM API Key]({{site.data.keyword.ref-con-presto-serv-link}}#get-ibmapi-key).
         {: note}

     - Use one of the following commands to connect to Milvus using IAM token:

         ```bash
         connections.connect(host="<host>", port="<port>", secure=True, user="ibmlhtoken", password="<token>")
         ```
         {: codeblock}

         or

        ```bash
        from pymilvus import MilvusClient, DataType

        milvus_uri = "https://<ibmlhtoken>:<token>@<host>:<port>"
        client = MilvusClient(
            uri=milvus_uri,
            secure=True
        )
         ```
         {: codeblock}

         Replace `<token>` with the IAM token. For information about getting a token, see [Getting IBM Access Management (IAM) token]({{site.data.keyword.ref-con-presto-serv-link}}#get-ibmiam-token).
         {: note}

     - Use one of the following commands to connect to Milvus using Uniform Resource Identifier (URI):

         ```bash
         print(fmt.format("start connecting to Milvus"))
         connections.connect( alias="default", uri="https://<host>:<grpc-port>", user = "ibmlhtoken", password = "<token>" )
         has = utility.has_collection("hello_milvus")
         print(f"Does collection hello_milvus exist in Milvus: {has}")
         ```
         {: codeblock}

         or

         ```bash
        from pymilvus import MilvusClient, DataType

        milvus_uri = "https://<ibmlhapikey>:<api-key>@<host>:<port>"
        client = MilvusClient(
            uri=milvus_uri,
            secure=True
        )
         ```
         {: codeblock}

        Replace `<token>` with the IAM token. For information about getting a token, see [Getting IBM Access Management (IAM) token]({{site.data.keyword.ref-con-presto-serv-link}}#get-ibmiam-token).
         {: note}

1. To make REST API calls using Milvus REST route, see [RESTful API reference](https://milvus.io/api-reference/restful/v2.5.x/About.md).

    For example, use the following command to list all the collections:

    ```bash
    curl --request GET \
        --url "https://<REST-host>:<REST-port>/v1/vector/collections" \
        --header "Authorization: Basic $(echo -n '<user>:<password>' | base64)" \
        --header "Content-Type: application/json"
    ```
    {: codeblock}


## What to do next
{: #postreq}

You can perform the following operations after establishing a connection with a Milvus service:

- **Manage data**

    - You can insert, upsert, or delete data in the Milvus service. For more information, see [Insert, Upsert & Delete](https://milvus.io/docs/insert-update-delete.md).
    - You can import data from Milvus. For more information, see [Prepare and import data](https://milvus.io/docs/prepare-source-data.md)

- **Manage databases**: You can create databases in Milvus and allocate privileges to certain users to manage them. A Milvus cluster supports a maximum of 64 databases. For more information, see [Manage Databases](https://milvus.io/docs/manage_databases.md).
- **Manage collections**: You can create and manage collections using the SDK of your choice. A Milvus cluster supports a maximum of 65,536 collections. For more information, see [Manage Collections](https://milvus.io/docs/manage-collections.md#Manage-Collections).
- **Manage partitions**: You can create and manage partitions in a collection. A Milvus cluster supports a maximum of 4095 partitions. For more information, see [Manage Partitions](https://milvus.io/docs/manage-partitions.md#Manage-Partitions).
- **Manage indexes**: You can creating and managing indexes on vector fields in a collection. For more information, see [Manage Indexes](https://milvus.io/docs/index-vector-fields.md?tab=floating).
- **Search and Query**: For information searching and querying data in Milvus, see [Search, Query & Get](https://milvus.io/docs/single-vector-search.md).

## Related API
{: #connmilvus_api}

For information on related API, see
* [Get Milvus service](https://cloud.ibm.com/apidocs/watsonxdata#get-milvus-service)
* [Delete Milvus service](https://cloud.ibm.com/apidocs/watsonxdata#delete-milvus-service)
* [Update Milvus service](https://cloud.ibm.com/apidocs/watsonxdata#update-milvus-service)
* [Get Milvus service databases](https://cloud.ibm.com/apidocs/watsonxdata#list-milvus-service-databases)
* [Get Milvus database collections](https://cloud.ibm.com/apidocs/watsonxdata#list-milvus-database-collections)
* [Scale a Milvus service](https://cloud.ibm.com/apidocs/watsonxdata#create-milvus-service-scale)
