---

copyright:
  years: 2022, 2024
lastupdated: "2024-09-30"

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
- Authorized user credentials to access the Milvus instance.
- Assign a role to the user or [service ID](https://cloud.ibm.com/docs/account?topic=account-serviceids&interface=ui) from **Infrastructure manager**. For more information about user roles, see [Managing roles and privileges]({{site.data.keyword.ref-role_priv-link}}#milvus){: external}.

## By using API key
{: #conn-to-milvusapikey}

- For REST API calls:

    ```bash
    print(fmt.format("start connecting to Milvus"))
    connections.connect(host="<host>", port="<port>", secure=True, user="apikey", password="<api-key>")
    has = utility.has_collection("hello_milvus")
    print(f"Does collection hello_milvus exist in Milvus: {has}")
    ```
    {: codeblock}

- For GRPC calls:

    ```bash
    print(fmt.format("start connecting to Milvus"))
    connections.connect(host="<host>", port="<port>", secure=True, user="ibmlhapikey", password="<api-key>")
    has = utility.has_collection("hello_milvus")
    print(f"Does collection hello_milvus exist in Milvus: {has}")
    ```
    {: codeblock}

## By using Token
{: #conn-to-milvusatoken}

```bash
connections.connect(host="<host>", port="<port>", secure=True, server_name="localhost", user="ibmlhtoken", password="<token>")
```
{: codeblock}

For more information about getting a token, see [Getting IBM Access Management (IAM) token]({{site.data.keyword.ref-con-presto-serv-link}}#get-ibmiam-token){: external}.

## By using URI
{: #conn-to-milvusuri}

This is an alternate method of connecting to Milvus without using the `host` and `port` parameters.
{: note}

```bash
print(fmt.format("start connecting to Milvus"))
connections.connect( alias="default", uri="https://<host>:<grpc-port>", user = "ibmlhtoken", password = "token" )
has = utility.has_collection("hello_milvus")
print(f"Does collection hello_milvus exist in Milvus: {has}")
```
For getting API keys, see [Getting the IBM API key]({{site.data.keyword.ref-con-presto-serv-link}}#get-api-iam-token){: external}.

## What to do next
{: #postreq}

You can perform the following operations after establishing a connection with a Milvus service:

- **Manage databases**: A Milvus cluster supports a maximum of 64 databases. For more information, see [Manage Databases](https://milvus.io/docs/manage_databases.md).
- **Manage collections**: A Milvus cluster supports a maximum of 65,536 collections. For more information, see [Manage Collections](https://milvus.io/docs/manage-collections.md#Manage-Collections).
- **Manage partitions**: A Milvus cluster supports a maximum of 4095 partitions. For more information, see [Manage Partitions](https://milvus.io/docs/manage-partitions.md#Manage-Partitions).
- **Manage data**: For more information, see:
      - [Insert, Upsert & Delete](https://milvus.io/docs/insert-update-delete.md)
      - [Data Import](https://milvus.io/docs/prepare-source-data.md)
- **Manage indexes**: For more information, see [Manage Indexes](https://milvus.io/docs/index-vector-fields.md?tab=floating).
- **Search and Query**: For more information, see [Search, Query & Get](https://milvus.io/docs/single-vector-search.md).
